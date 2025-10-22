
철학 : 처음부터 설명, 빠른 데모, 낮은 인지코스트 -- 능동적 활용 도모

대상 : sui해커톤 참가자 -- move언어 기초수준 .. 교육자료 첨부

MVP 수준: 완성된 DApp

홍보문구: 이제 블록체인은 product다. 이걸 위해선 nodit은 최고의 선택이다.

30초 안에 첫 번째 결과 확인 > 이후 5분 퀵스타트로 API 연결 확인

조합 가능한 모듈들 제공, "이런 앱을 만들려면?" 가이드



개요, 목차

cheat sheet 목적

노딧 소개

사이트 소개

노딧을 사용해야하는 이유 / 주요 메서드 소개

mcp소개 https://developer.nodit.io/docs/nodit-mcp

코드스니펫 소개 -- 간단한 데모, 링크 -- 처음 시작하는 사람의 관점에서

FAQ

마무리 멘트


기능 : 영어, 한국어, 링크


nodit cheat sheet --sui
노딧을 이용해 빠르게 빌드하고, 분석하세요!

what is Nodit?
Nodit은 Lambda256에서 개발한 블록체인 인프라 서비스로, 개발자들이 별도의 노드 운영 없이 안정적인 블록체인 API를 사용할 수 있게 해주는 BaaS(Blockchain as a Service) 플랫폼입니다. 개발자들이 복잡한 블록체인 인프라를 직접 구축하지 않고도 필요한 데이터를 쉽고 빠르게 추출할 수 있도록 하는 것이 핵심 가치입니다.

노딧을 이용하면 기존 블록체인 서비스를 만들기 전 필요한 블록체인 네트워크 설정, 노드 셋업, 데이터 싱크업 등의 과정을 획기적으로 줄이고, 서비스 개발 이후의 노드 운영, 이벤트 모니터링 등 블록체인 인프라 레벨 시스템에 신경 쓸 필요 없이 서비스 운영에만 집중할 수 있습니다.

현재 upbit를 포함한 국내 3개의 거래소가 nodit의 서비스를 이용하고 있으며 24/7 모니터링 시스템과 즉각대응 시스템으로 어떤 장애가 발생해도 안정적으로 운영할 수 있습니다.

**주요 특징:**

- **다중 체인 지원**: Ethereum, Sui, Polygon, Arbitrum, Solana 등 20개 이상의 블록체인 네트워크 지원
- **개발자 친화적 API**: RESTful API와 GraphQL을 통해 블록체인 데이터 조회, 트랜잭션 전송, 스마트 컨트랙트 호출 등을 간편하게 처리
- 빠른 실행: [nodit.lambda256.io](https://nodit.lambda256.io)에서 회원가입 후 API 키 발급받아 무료로 즉시 사용 가능합니다.


when?
다음은 주요 프로젝트들에 대한 api 사용 예시입니다.
### 1. ** NFT 기반 게임 플랫폼**

**핵심 API 조합:**

- `suix_getOwnedObjects` → 플레이어의 게임 아이템(NFT) 인벤토리 표시
- `sui_getNormalizedMoveModule` → 게임 컨트랙트 로직 분석 및 시각화
- `unsafe_moveCall` → 아이템 강화, 전투, 합성 등 게임 액션 실행
- `suix_queryEvents` → 실시간 게임 로그, 레벨업 알림

**완성품**: 플레이어가 NFT 캐릭터로 전투하고, 아이템을 거래하는 실시간 RPG

---

### 2. DeFi 대시보드 & 자동 투자**

**핵심 API 조합:**

- `suix_getAllBalances` → 사용자 포트폴리오 실시간 추적
- `suix_getValidatorsApy` → 최적 스테이킹 풀 추천
- `suix_getTotalSupply` → 토큰 공급량 기반 투자 분석
- `unsafe_requestAddStake` → 원클릭 자동 스테이킹

**완성품**: 최고 수익률 자동 찾기 + 분산 투자 + 실시간 수익 알림 앱

---

### 3. ** 크로스체인 소셜 플랫폼**

**핵심 API 조합:**

- `suix_resolveNameServiceAddress` → Sui 도메인으로 소셜 프로필 생성
- `suix_getDynamicFields` → 사용자 포스트, 팔로워 데이터 관리
- `suix_subscribeEvent` → 실시간 댓글, 좋아요 알림
- `unsafe_transferSui` → 크리에이터 후원, 팁 기능

**완성품**: Web3 트위터 + 크리에이터 이코노미 + NFT 프로필 시스템


전체기능은 여기에서 확인하세요
https://developer.nodit.io/reference/sui_devinspecttransactionblock


how?
AI, LLM 도구를 사용하여 Nodit을 더 쉽고 빠르게 연동할 수 있습니다. 
Nodit 개발자 문서가 지원하는 다양한 AI 연동 방식을 확인하세요.
https://developer.nodit.io/docs/using-nodit-with-ai-llm-tools

Nodit MCP를 직접 AI 도구나 LLM에 연동하여 AI가 직접 API Reference를 조회하고 실시간으로 호출하여 데이터를 활용할 수 있습니다.
https://developer.nodit.io/docs/nodit-mcp


quick start
예시 프로젝트입니다. 이 레포지토리를 통해 nodit의 api가 어떻게 동작하는 지 확인해보세요. 
https://github.com/nubro999/hackathon_info


이제 api를 발급받고 nodit을 이용해 프로젝트를 빠르고 쉽게 빌드하세요!
https://developer.nodit.io/docs/get-started-with-nodit


nodit에서 제공하는 전체 Sui API를 기능 영역별로 분류한 목록과 각 API의 상세 설명입니다. 이곳에서 API의 요구사항, 입력 매개변수, 출력 형식을 상세하게 확인할 수 있습니다.
https://developer.nodit.io/reference/sui-quickstart 


**개발/테스트 도구**

- `sui_devInspectTransactionBlock`: 트랜잭션 시뮬레이션 (상세 분석)
- `sui_dryRunTransactionBlock`: 트랜잭션 드라이런 (실행 전 검증)

**실제 실행**

- `sui_executeTransactionBlock`: 트랜잭션 실제 실행 및 블록체인 커밋

## 2. 블록체인 상태 조회

**체인 정보**

- `sui_getChainIdentifier`: 체인 식별자 조회
- `sui_getProtocolConfig`: 프로토콜 설정 정보
- `sui_getTotalTransactionBlocks`: 총 트랜잭션 블록 수

**체크포인트 관련**

- `sui_getCheckpoint`: 특정 체크포인트 조회
- `sui_getCheckpoints`: 여러 체크포인트 조회
- `sui_getLatestCheckpointSequenceNumber`: 최신 체크포인트 번호

## 3. 객체 및 데이터 조회

**객체 조회**

- `sui_getObject`: 단일 객체 조회
- `sui_multiGetObjects`: 여러 객체 일괄 조회
- `sui_tryGetPastObject`: 과거 객체 상태 조회
- `sui_tryMultiGetPastObjects`: 여러 과거 객체 상태 조회

**트랜잭션 조회**

- `sui_getTransactionBlock`: 특정 트랜잭션 블록 조회
- `sui_multiGetTransactionBlocks`: 여러 트랜잭션 블록 조회

**이벤트**

- `sui_getEvents`: 이벤트 조회

## 4. Move 언어 관련 (스마트 컨트랙트)

**함수 정보**

- `sui_getMoveFunctionArgTypes`: Move 함수 인수 타입
- `sui_getNormalizedMoveFunction`: 정규화된 Move 함수

**모듈 정보**

- `sui_getNormalizedMoveModule`: 정규화된 Move 모듈
- `sui_getNormalizedMoveModulesByPackage`: 패키지별 Move 모듈들
- `sui_getNormalizedMoveStruct`: 정규화된 Move 구조체

## 5. SUIX - 확장 기능들

**잔액 및 코인 관리**

- `suix_getAllBalances`: 모든 토큰 잔액
- `suix_getAllCoins`: 모든 코인 조회
- `suix_getBalance`: 특정 토큰 잔액
- `suix_getCoinMetadata`: 코인 메타데이터
- `suix_getCoins`: 코인 조회
- `suix_getTotalSupply`: 총 공급량

**소유권 및 객체**

- `suix_getOwnedObjects`: 소유 객체 조회
- `suix_getDynamicFieldObject`: 동적 필드 객체
- `suix_getDynamicFields`: 동적 필드들

**스테이킹 관련**

- `suix_getStakes`: 스테이킹 정보
- `suix_getStakesByIds`: ID별 스테이킹 정보
- `suix_getValidatorsApy`: 검증자 APY
- `suix_getCommitteeInfo`: 위원회 정보
- `suix_getLatestSuiSystemState`: 최신 Sui 시스템 상태

**가격 및 시스템**

- `suix_getReferenceGasPrice`: 기준 가스 가격

**검색 및 쿼리**

- `suix_queryEvents`: 이벤트 쿼리
- `suix_queryTransactionBlocks`: 트랜잭션 블록 쿼리

**네임 서비스**

- `suix_resolveNameServiceAddress`: 이름 → 주소 해석
- `suix_resolveNameServiceNames`: 주소 → 이름 해석

**구독 (실시간)**

- `suix_subscribeEvent`: 이벤트 구독
- `suix_subscribeTransaction`: 트랜잭션 구독

## 6. UNSAFE - 트랜잭션 생성 도구들

**코인 관리**

- `unsafe_mergeCoins`: 코인 병합
- `unsafe_splitCoin`: 코인 분할
- `unsafe_splitCoinEqual`: 코인 균등 분할

**전송**

- `unsafe_transferObject`: 객체 전송
- `unsafe_transferSui`: SUI 토큰 전송
- `unsafe_pay`: 결제
- `unsafe_payAllSui`: 모든 SUI 결제
- `unsafe_paySui`: SUI 결제

**스마트 컨트랙트**

- `unsafe_moveCall`: Move 함수 호출
- `unsafe_publish`: 컨트랙트 배포

**스테이킹**

- `unsafe_requestAddStake`: 스테이킹 추가 요청
- `unsafe_requestWithdrawStake`: 스테이킹 출금 요청

**일괄 처리**

- `unsafe_batchTransaction`: 배치 트랜잭션

**인증**

- `sui_verifyZkLoginSignature`: zkLogin 서명 검증

Nodit에서 개발을 시작하는 가장 쉽고 빠른 방법입니다.  
MCP를 활용하여 지갑 활동, 온체인 트랜잭션, NFT 등의 정보를 자연어로 분석하고 활용할 수 있으며, 이를 AI 에이전트나 자동화된 워크플로우와 연동할 수 있습니다.


Application Layer
    ↓
[HTTP Data: "GET /index.html"]
    ↓
Transport Layer
    ↓
[TCP Header][HTTP Data]
    ↓
Network Layer
    ↓
[IP Header][TCP Header][HTTP Data]
    ↓
Link Layer
    ↓
[Ethernet Header][IP Header][TCP Header][HTTP Data][Ethernet Trailer]
    ↓
Physical Layer
    ↓
01010101010101... (전기 신호)
