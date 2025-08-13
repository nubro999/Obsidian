

다음은 Sui 네트워크(온체인 Move 로직, 별도 전통 백엔드 없음)에서 2인 “땅따먹기 / 토큰 수집” 게임을 만들 때의 프론트엔드 전체 아키텍처 설계 가이드입니다.  
목표:  
- 모든 핵심 게임 상태(맵, 토큰, 플레이어 진행)를 Move 컨트랙트 기반 온체인 객체로 관리  
- 프론트는 지갑 연결 + 트랜잭션 전송 + 이벤트 구독 + 캔버스 렌더 + 낙관적(optimistic) UI  
- 도트(pixel art) 스타일, 반응성 있는 UX, 체인 지연(latency) 보완

--------------------------------
1. 전반적 구조 개요
--------------------------------
레이어 구분:
1) Wallet / Chain Access Layer  
 - Sui Wallet Adapter (숏컷: @mysten/sui.js + 지갑 어댑터 패키지)  
 - 트랜잭션 빌드, 서명, 전송  
 - Sui 이벤트/오브젝트 구독 (WebSocket)  

2) Game State Sync Layer  
 - 온체인 객체(GameInstance, Map, Token, Player) -> 클라이언트 캐싱  
 - 이벤트(Event) → 로컬 상태 머지  
 - 폴백: 주기적 폴링 (ex: 5~10초)  
 - 낙관적 업데이트(Optimistic)와 확정(Confirmed) 상태 이원화

3) Domain Model Layer  
 - 맵 좌표 변환, 토큰 인덱싱 (coordinate → tokenId), 충돌/획득 규칙  
 - 온체인 sequence / tick 기반 순서 일관성 관리

4) UI State / Store Layer  
 - Zustand 또는 Jotai (경량, recoil보다 단순), 혹은 Redux Toolkit  
 - 구분: immutable static (맵 크기, 타일 시트 정보) vs reactive dynamic (플레이어 위치, 획득된 토큰)

5) Rendering Layer  
 - HTMLCanvas 2D 또는 Pixi.js (간단한 스프라이트, 텍스처 batching)  
 - Pixel Art Tips:
   - CSS: image-rendering: pixelated  
   - 내부 타일 크기를 16x16 또는 8x8 기준, 캔버스 확대(scale)  
   - OffscreenCanvas(지원 브라우저 한정) → 부드러운 프레임  
 - requestAnimationFrame 루프 (UI smooth), 로직 결정은 온체인/이벤트 기준

6) Input / Command Layer  
 - 키 입력 (WASD/Arrow) → 이동 커맨드 -> 낙관적 위치 이동 → Move 호출 트랜잭션 enqueued  
 - UI debounce (ex: 200~300ms) 또는 Tick 단위(턴 기반)로 제한

7) Error & Conflict Handling  
 - 트랜잭션 실패 시 낙관적 반영 되돌리기  
 - 동일 토큰 경합: 체인 결과(event)로 최종 소유자 확정

--------------------------------
2. 온체인 객체 설계(프론트 입장에서 필요한 뷰 모델)
--------------------------------
프론트가 필요로 하는 직렬화/구조(요약):


가스/성능 최적화:
- 전체 맵을 한 번에 업데이트하지 말고 ‘토큰 개별 객체’ 또는 ‘Chunk Object (예: 16x16 영역)’ 단위로 소유/획득 상태만 변경  
- 토큰 획득 시: player.score 증가 + token.claimed true (혹은 토큰 소유권 이전)  
- Move 함수: move_player(game_id, direction, client_seq)  
  - 서버가 없으므로 순서 보장: client_seq > stored last_seq 면 갱신  
  - 이벤트 발행: PlayerMoved {player_id, x, y, seq}  
- 토큰 획득: capture_token(game_id, token_id, player_id) → TokenCaptured 이벤트

프론트 이벤트 구독 매핑:
- PlayerMoved → 해당 플레이어 위치 업데이트  
- TokenCaptured → 토큰 상태 claimed, UI 점수 업데이트  
- GameStarted / GameFinished → 단계 전환  

--------------------------------
3. 실시간성 전략
--------------------------------
문제: 완전 온체인 상호작용은 블록/최종화 지연(수 초) → 즉각적 반응 감소  
해결 옵션:
A) 낙관적 이동  
 - 키 입력 -> 로컬 좌표 즉시 이동 (optimistic)  
 - 트랜잭션 전송  
 - 이벤트 수신 후 confirmed 플래그  
 - 불일치 시 롤백 (스냅샷 저장 후 diff revert)  

B) Tick 기반 (Turn / Fixed Step)  
 - 예: 500ms마다 1 tick 허용 → 그 안의 중복 입력은 마지막 방향만 적용  
 - 체인 Move 함수가 tick 검증 (현재 tick과 예측 tick 일치)  

C) Commit-Reveal (치트 방지 강화 필요 시)  
 - 플레이어가 해시로 의도 제출(commit) 후 reveal → 이 게임은 단순 이동이므로 과도할 수 있음  

추천: 초기 MVP에는 A + 간단 rate limit. 이후 공정성 문제가 커지면 Tick 구조로 전환.

--------------------------------
4. 프론트엔드 기술 스택 제안
--------------------------------
- 언어/프레임워크: React + TypeScript + Vite  
- 상태 관리: Zustand (간단한 store + 미들웨어로 optimistic/rollback)  
- 렌더링:  
  - 간단 → Canvas 2D  
  - 이펙트/레이어 많음 → Pixi.js  
- 스타일/UI: Tailwind CSS (HUD, 패널)  
- Sui 연동: @mysten/sui.js, wallet adapter (Sui Wallet, Ethos, etc.)  
- 빌드: Vite + 환경변수(.env)로 RPC/WS endpoint  
- 테스팅: Vitest + Playwright(시나리오: 두 탭 시뮬레이션)  
- 개발 편의: 소규모 로컬 mock (토큰 및 이동 fake generator) → 체인 없는 UI 테스트

--------------------------------
5. 디렉터리 구조 예시
--------------------------------


--------------------------------
6. 상태(Store) 설계
--------------------------------
구분:
- staticState: width, height, tileSize
- dynamicState: players{}, tokens{} (claimed, owner), gamePhase, localPlayerId
- optimisticQueue: { seq, actionType, appliedAt, revertSnapshot }
- connection: walletAddress, chainStatus, subscribing 여부

Zustand 예시 (간단 축약):


--------------------------------
7. 이벤트 구독 (WebSocket)
--------------------------------
Sui JS SDK: client.subscribeEvent({ filter, onMessage })

예시 (PlayerMoved / TokenCaptured):

````typescript
import { SuiClient } from '@mysten/sui.js/client';
import { useGameStore } from '../game/state/store';

export function subscribeGameEvents(client: SuiClient, gameId: string) {
  // PlayerMoved
  client.subscribeEvent({
    filter: {
      MoveEventType: '0x<package_id>::game::PlayerMoved'
    },
    onMessage(ev) {
      if (!('parsedJson' in ev)) return;
      const pj = ev.parsedJson as any;
      if (pj.game_id !== gameId) return;
      useGameStore.getState().confirmMove({
        playerId: pj.player_id,
        chainSeq: Number(pj.seq),
        x: Number(pj.x),
        y: Number(pj.y)
      });
    }
  });

  // TokenCaptured
  client.subscribeEvent({
    filter: {
      MoveEventType: '0x<package_id>::game::TokenCaptured'
    },
    onMessage(ev) {
      if (!('parsedJson' in ev)) return;
      const pj = ev.parsedJson as any;
      if (pj.game_id !== gameId) return;
      useGameStore.setState(state => {
        const t = state.tokens[pj.token_id];
        if (t) {
          t.claimed = true;
          t.owner = pj.player_id;
        }
        const pl = state.players[pj.player_id];
        if (pl) pl.score += Number(pj.value);
      });
    }
  });
}
````

--------------------------------
8. 이동 트랜잭션 빌드/전송
--------------------------------
Move 함수 예시 시그니처 (가정):
public entry fun move_player(game: &mut GameInstance, player: &mut Player, direction: u8, client_seq: u64, ctx: &mut TxContext)

프론트:

````typescript
import { Transaction } from '@mysten/sui.js/transactions';
import { useWallet } from '@mysten/wallet-adapter-react';

export async function submitMove({gameId, playerId, direction}: {
  gameId: string; playerId: string; direction: number;
}) {
  // direction: 0 up,1 right,2 down,3 left 등
  const { signAndExecuteTransaction } = useWallet();
  const tx = new Transaction();
  tx.moveCall({
    target: '0x<package>::game::move_player',
    arguments: [
      tx.object(gameId),
      tx.object(playerId),
      tx.pure.u8(direction),
      tx.pure.u64(Date.now()) // 임시 client_seq (더 나은 seq 관리 필요)
    ]
  });
  return signAndExecuteTransaction({ transaction: tx });
}
````

입력 처리 (낙관적 + 트랜잭션 큐):
````typescript
import { useGameStore } from '../game/state/store';
import { submitMove } from '../chain/tx/move';

const DIR_MAP = {
  ArrowUp: {dx:0, dy:-1, dir:0},
  ArrowRight: {dx:1, dy:0, dir:1},
  ArrowDown: {dx:0, dy:1, dir:2},
  ArrowLeft: {dx:-1, dy:0, dir:3}
};

export function handleKey(e: KeyboardEvent, playerId: string, gameId: string) {
  const d = DIR_MAP[e.key as keyof typeof DIR_MAP];
  if (!d) return;

  // Optimistic
  useGameStore.getState().applyOptimisticMove({playerId, dx: d.dx, dy: d.dy});

  submitMove({gameId, playerId, direction: d.dir})
    .catch(err => {
      console.error('move tx fail', err);
      // 롤백: 마지막 낙관 move 찾기
      const st = useGameStore.getState();
      const last = [...st.optimistic.pendingMoves].reverse()
        .find(m => m.playerId === playerId);
      if (last) st.rollback(last.localSeq);
    });
}
````

--------------------------------
9. 캔버스 렌더링 루프
--------------------------------
렌더 특징:
- Logic update는 이벤트 기반, 렌더는 requestAnimationFrame  
- 플레이어/토큰 스프라이트: 작은 atlas  
- 카메라(맵이 클 경우) = viewport offset

--------------------------------
10. 동시성 & 충돌 처리 상세
--------------------------------
문제 시나리오: 두 플레이어가 거의 동시에 같은 토큰 좌표로 이동 → 누가 먼저 캡쳐?  
솔루션:
- TokenCaptured 함수 내에서 토큰이 아직 unclaimed인지 체크 → 첫 성공만 이벤트 발생  
- 플레이어 이동 후 캡쳐는 별도 호출이면 지연 가능 → Move 함수 내부에 “해당 위치 토큰이 있으면 즉시 캡쳐” 포함해 원자화  
- sequence / tick: PlayerMoved 이벤트의 seq 필드(컨트랙트에서 증가) → 프론트가 낙관적 seq와 매칭  
- 불일치: 프론트 seq > 체인 seq(말이 안 됨) → 전체 플레이어 상태 재동기화 (fetch objects)

재동기화 트리거:
- 이벤트 파싱 실패
- 연속 n회 트랜잭션 실패
- ‘드리프트’ 감지(낙관적 이동 5개 이상 미확정)  
→ fetchGameSnapshot()

--------------------------------
11. 스냅샷 재동기화
--------------------------------
체인에서:
- getObject(game_id) -> GameInstance
- getDynamicFields(map) → 토큰 목록 페이징
- getObject(player_id) each

최적화:
- 초기 로딩: 한번에 병렬 fetch → 변환 후 store.set  
- 이후: 이벤트 기반 증분  
- 주기: 30~60초 풀 스냅샷 검증 (오류 누적 방지)

--------------------------------
12. 가스 / UX
--------------------------------
- 이동이 잦은 경우 가스 부담 → 게임 규칙을 ‘제한된 이동 횟수 / tick’으로 설계  
- 또는 Sponsorship(가스 대납) 구조 고려 (Sui sponsor transaction)  
- 플레이 세션 종료 후 점수 정산 1회 트랜잭션 등으로 압축? (그러나 실시간 토큰 획득 의미 감소)  
- MVP는 단순: 한 이동당 하나 트랜잭션 + 캡쳐 포함

--------------------------------
13. 보안 / 치트 대응
--------------------------------
- 로컬단에서 좌표 범위 체크 (시각적)하더라도 최종 권한은 Move 검증  
- Move 함수:
  - direction 값 검증 (0~3)
  - 이동 후 좌표 맵 경계 검사
  - client_seq > 저장 seq → 업데이트; 아니면 무시 (replay 방지)
- 토큰 중복 획득 방지: token.claimed assert
- 빠른 연속 이동(스팸) 방지: last_move_time + 최소 간격 (컨트랙트 필드)

--------------------------------
14. 개발 워크플로
--------------------------------
1) Move 모듈: 작은 단일 기능부터 (GameInstance 생성, Player 등록, 단일 이동)  
2) 프론트: Mock store → Canvas 테스트  
3) Wallet 연결 → 실제 Move 호출 → 이벤트 subscription 연결  
4) 낙관적 로직 추가 및 롤백 테스트  
5) 토큰 생성 & 캡쳐 추가  
6) 마지막: 스타일링(HUD, 점수판, 연결 상태 뱃지)

--------------------------------
15. 성능 / 최적화 포인트
--------------------------------
- 이벤트 폭주 시 디바운스(예: requestAnimationFrame batching)  
- 큰 맵: Chunking (visible chunk만 draw)  
- Token 색상 / 스프라이트 atlas 사전 로드  
- Object fetch 캐시 (id → 메모리) + ETag처럼 version(seq) 관리

--------------------------------
16. 향후 확장 아이디어
--------------------------------
- WebRTC DataChannel P2P를 통한 실시간 예측 공유 (체인 최종화 전 플레이어 위치 교환)  
- Spectator 모드 (읽기 전용 이벤트)  
- 점수 랭킹: 별도 인덱서 or The Graph 유사 서비스 (추후 백엔드 최소화)  
- 애니메이션(이동 tween), 파티클(픽셀 폭발) Pixi.js 적용  

--------------------------------
17. 빠른 실행 체크리스트
--------------------------------
- [ ] Move: create_game, join_game, move_player(내부 캡쳐 포함)  
- [ ] 이벤트: PlayerMoved, TokenCaptured, GameStarted, GameFinished  
- [ ] TS 타입 매핑  
- [ ] Zustand store 초안 + optimistic API  
- [ ] WalletConnect 컴포넌트  
- [ ] subscribeGameEvents 연결  
- [ ] 캔버스 기본 렌더 + 키입력 핸들러  
- [ ] 롤백 시나리오 테스트 (트랜잭션 실패 강제)  
- [ ] 맵/토큰 초기 fetch + 주기 sync  

--------------------------------
18. 결론
--------------------------------
중앙 백엔드 없이도 Sui의 이벤트 + 객체 모델 + 낙관적 UI 기법을 활용하면 가벼운 2인 땅따먹기 게임을 구현할 수 있습니다. 핵심은:
- 맵/토큰을 ‘세분화된 객체’로 설계해 변경 비용 최소화
- 이동/획득을 원자적 Move 함수로 처리
- 프론트는 낙관적 상태와 체인 확정 상태를 명확히 분리
- 주기적 스냅샷으로 동기화 신뢰성 확보
- Canvas/Pixi로 도트 스타일 구현
