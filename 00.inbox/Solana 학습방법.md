
필수:

- 프로그래밍 언어: Rust (Ownership, Borrowing, Lifetime, Traits, Result/Error, Option, Cargo)
- 기본 암호학: 해시(Hash), 공개키/비밀키, 서명(Signature), 키페어(Keypair)
- 블록체인 일반: 트랜잭션, 블록, 상태(State), 계정(Account) 개념
- 병렬 처리/트랜잭션 격리 기본(낙관적 동시성, 잠금 충돌)

있으면 매우 도움:

- EVM 스마트컨트랙트 경험 (차이점 대비 학습 충격 ↓)
- 데이터 직렬화(Serialization; Borsh / JSON / MessagePack)
- 시스템 프로그래밍 감각 (메모리, 구조체 패킹)

Rust 학습 추천 흐름(최소 커트라인):

1. The Rust Book 챕터 4(Ownership), 5(Struct), 6(Enum), 8(Collections), 9(Error Handling), 10(Generic/Trait), 11(Test), 13(Iterator)
2. Result / Option 패턴 → Solana Program 안에서 unwrap 금지 습관화
3. cargo test / feature flag / workspace 사용법

---

2. Solana 코어 개념 맵

---

핵심 키워드(영/한/요약):

- Account / 계정: EVM storage와 달리 모든 상태는 Account에 저장. 코드도 Program Account.
- Program / 프로그램: on-chain 실행 바이너리 (BPF). EVM의 Contract에 해당.
- Instruction / 명령: 트랜잭션 내 단일 호출 단위(Program 호출 파라미터 + Account 리스트).
- Transaction / 트랜잭션: Instruction들의 묶음. 모든 필요한 Account 선명시 필수.
- Runtime (Sealevel): 계정 읽기/쓰기 집합을 보고 병렬 실행 가능하도록 스케줄링.
- PDA (Program Derived Address, 프로그램 파생 주소): 시드 + Program ID로 생성되는, 비밀키 없이 Program이 서명 권한처럼 사용하는 주소.
- CPI (Cross Program Invocation): 다른 Program 호출 (EVM delegatecall과 개념 차이 존재).
- Rent / 임대료: 움직임 없는 계정은 임대 소멸 가능. rent-exempt(최소 잔고 유지) 전략 필수.
- Compute Units: 실행 비용 한도. 복잡한 연산 → 증가 → CU 제한 최적화 필요.
- Borsh / Anchor IDL: 데이터 직렬화 표준.
- Anchor Framework: 개발 보일러플레이트 감소(어노테이션, IDL 생성, 에러 코드 정의, PDA 간소화).
- Token Program (SPL Token): Fungible 토큰 표준 구현 (EVM ERC-20에 대응).
- Associated Token Account (ATA): 지갑 + Mint 조합의 표준 토큰 보관 계정.
- Metaplex: NFT/Metadata/Token Metadata Program 등 생태계 표준.

---

3. Anchor vs Raw (Native) 선택 전략

---

- 빠른 프로토타입 / 생산성 / IDL 기반 프론트 연동 → Anchor
- 극한 최적화, Anchor 추상화 오버헤드 제거, 커스텀 직렬화 → Native (Raw) Solana Program 권장 학습 순서:

1. Native 예제 한 번 직접 (계정 파싱 / instruction 데이터 파싱 수동 경험)
2. Anchor로 재작성 → 생산성 체감
3. 이후 대부분 Anchor 사용, 특수 케이스만 Native

---

4. 환경 구축

---

1. Rust 설치: rustup (stable toolchain)
2. Solana CLI: solana --version
3. Local validator: solana-test-validator (로컬 체인)
4. Keypair 생성: solana-keygen new
5. Airdrop: solana airdrop 2 (로컬)
6. Anchor 설치: cargo install --git [https://github.com/coral-xyz/anchor](https://github.com/coral-xyz/anchor) avm && avm install latest && avm use latest
7. Anchor 프로젝트 초기화: anchor init myproj

Tip: workspace 구조에서 program/ 폴더 하위에 여러 프로그램 나눠 모듈화.

---

5. 단계별 실습 로드맵

---

(각 단계마다 “목표 / 필수 개념 / 결과물”)

A. Hello Program

- 목표: 단일 instruction, 로그 출력
- 개념: entrypoint, process_instruction 함수 / Anchor의 #[program] 차이
- 결과: “Hello” 로그, CI용 cargo test

B. Account State 저장

- 목표: 사용자 counter 증가
- 개념: Account 구조체, rent-exempt 계산(solona rent CLI), space 계산
- 결과: Anchor #[account] 구조체 / Native에서는 borsh derive

C. PDA

- 목표: 사용자별 PDA에 상태 저장 (seeds: user_pubkey + “profile”)
- 개념: find_program_address, bump
- 결과: Anchor seeds & bump 사용

D. SPL Token 연동

- 목표: 토큰 민트 + 전송
- 개념: Token Program ID, Mint Account, Token Account(ATA), CPI 호출
- 결과: 사용자가 instruction 호출 시 리워드 토큰 지급

E. Cross Program Invocation (CPI)

- 목표: 다른 Program 호출(예: Token Program) 또는 자신 Program 간 계층화
- 개념: invoke / invoke_signed, Anchor의 CpiContext
- 결과: safe transfer 함수

F. 에러 처리 / 보안

- 목표: 사용자 권한 체크
- 개념: Account ownership, signer 체크, replay 방지(계정 상태 값 nonce), time-based gating(Clock sysvar)
- 결과: 커스텀 에러 enum + require! 매크로(anchor)

G. 복합 트랜잭션

- 목표: 여러 instruction batch 트랜잭션 → front에서 accounts 정렬
- 개념: Client 측에서 Account Meta 구성, priority fee (최근 도입된 수수료 전략)

H. Off-chain + On-chain 통합

- 목표: 백엔드(예: Node.js / Typescript)에서 Program 호출, 이벤트 로그 파싱
- 개념: @solana/web3.js, Anchor client, IDL, subscription (connection.onProgramAccountChange)

I. NFT / Metadata (선택)

- 목표: Metadata Program 호출로 NFT 발행
- 개념: Token Metadata PDA, collection, creators array

J. 성능 / 최적화

- 목표: 계정 충돌 최소화 (병렬성)
- 개념: 동일 writable account 회피, 읽기 전용 계정 분리, 데이터 sharding(PDA seeds 다양화)
- 결과: 벤치마크(로컬 validator + --bpf-program)

K. 테스트 및 배포

- 목표: Devnet → Mainnet
- 개념: solana config set --url devnet, airdrop, anchor deploy, program upgrade authority 관리
- 결과: Upgrade authority 지갑 분리 / multisig 적용 (예: Squads)

L. 보안 검토

- 목표: 재진입(거의 불가하나 CPI 무한 루프), 서명자 체크, 계정 스푸핑 방지(seeds 검증)
- 개념: Instruction data 길이 검증, overflow (Rust 기본 safe), bump misuse 방지

---

6. 핵심 개념 심화 설명

---

1. Sealevel 병렬 실행

- 모든 Instruction은 (읽기계정 목록, 쓰기계정 목록)를 명시
- 두 Instruction이 같은 writable 계정을 공유하면 직렬화 (병목)
- 설계 전략: 상태를 여러 PDA에 분산: e.g. orderbook/“buckets”
- Anti-pattern: “global state” 단일 writable 계정 남발 → TPS 급락

2. PDA / 서명

- PDA는 실제 private key 없음
- Program이 invoke_signed로 seeds + bump 제공 시 “프로그램이 서명한 것과 동일”하게 인정
- 보안 포인트: seeds 재현 가능 → 악의적 주소 예측 / 중복 생성 여부 체크

3. Rent & Space

- 계정 생성 시 lamports = rent_exempt_threshold(space) 이상 넣어야 rent 면제
- Space 조정 불가(일반 계정) → 확장 필요 예상 시 versioning 또는 여러 PDA 체인 구조 설계

4. 직렬화

- Anchor는 자동(Borsh-like)
- Native에서: #[derive(BorshSerialize, BorshDeserialize)]
- 불변(Backward compatibility) 위해 struct 끝에만 새로운 필드 append (중간 삽입 → breaking)

5. Compute Unit 최적화

- 루프 최소화, heavy hash 함수 줄이기
- Anchor에서 remaining_accounts 활용 시 주석/정확한 ordering
- Feature: CU price 지정 (priority fee) → 혼잡 시 포함 확률 ↑

---

7. 학습용 추천 실전 미니 프로젝트

---

(난이도 상승 순)

1. Counter Program (기본)
2. Profile / Username Registry (PDA, 고유성)
3. Simple Token Faucet (SPL Mint + CPI)
4. Escrow / Atomic Swap (임시 PDA 계정에 토큰 보관 → 조건 충족 시 릴리즈)
5. Betting Game (결과값 오라클 입력 후 분배)
6. Order Matching Mini DEX (주문들을 PDA로 파편화 → 병렬성 테스트)
7. NFT Mint Launchpad (Whitelist, merkle root 검증)
8. Subscription / Streaming Payment (주기적 클레임, last_claimed timestamp 저장)
9. DAO Treasury (Multisig Program 연동, proposal PDA)
10. Cross-Program Aggregator (여러 Program CPI 호출, 체인 상 전략)

각 프로젝트마다:

- 설계 문서 (Account 구조 / PDA seeds / Instruction 목록)
- 실패 케이스 테스트 (권한 없는 계정, rent 부족, 잘못된 seeds, 중복 생성)

---

8. 코드 리딩(Reading) 전략

---

추천 리포지토리:

- spl-token (Token Program)
- metaplex-foundation / token-metadata
- marginfi / drift / jupiter(aggregator) 일부 읽는 순서:

1. Instruction enum / ID 정의 → entrypoint에서 dispatch 흐름 파악
2. Account parsing 부분(Anchor의 #[derive(Accounts)] / Native의 unpack)
3. PDA seeds 정의 위치(Anchor: #[account(seeds=..., bump)])
4. 에러 코드 설계(Error enum)
5. State 크기 계산 및 space 상수 선언 위치  
    노트: “왜 이 계정을 writable로 요구하는가?”를 모두 주석으로 답해보는 식의 적극적 독해.

---

9. Anchor 사용 시 주요 패턴

---

- #[program] mod program_name {...}: instruction 함수
- Context<YourAccountsStruct>: 계정 검증
- #[account(mut, seeds=[b"seed", user.key().as_ref()], bump)]
- init / realloc (realloc은 최근 anchor 기능, lamports 추가 필요)
- Anchor 에러: #[error_code] enum → require!(조건, 에러)
- Events: #[event] struct → client subscribe

---

10. 테스트 전략

---

- 단위 테스트: anchor test (Mocha + TS) 또는 Rust 기반 @solana-program-test
- 시나리오:
    1. 정상 흐름
    2. 잘못된 signer
    3. 계정 순서 바뀐 경우 실패
    4. rent 부족
    5. duplicate PDA 재생성 시도
    6. concurrency: 동일 writable 계정 접근 충돌 (두 트랜잭션 보내보고 하나 실패 확인)

---

11. 보안 체크리스트 (요약)

---

- PDA seeds 정확한 벨리데이션 (특히 사용자 제공 seed 일부 혼합 시)
- unchecked account casting 금지
- sysvar 계정(Clock, Rent) 주소 하드코딩 혹은 검증
- Upgrade authority 분리 (multisig) / production 이전 revoke 결정
- 재입력 공격? (대부분 read-modify-write 패턴에서 동일 트랜잭션 내 보호)
- lamports 인출 시 대상 계정이 기대한 Program ID 인지 검증
- CPI 호출 시 전달 account metas 의도 확인

---

12. 학습 타임라인 예시 (주 10~12시간 기준)

---

Week 1: Rust 기초 + Solana CLI + Hello Program  
Week 2: Account / PDA / Counter & Profile / Rent 개념  
Week 3: SPL Token / CPI / Faucet / Escrow  
Week 4: Anchor 전환 / 에러 처리 / 권한 패턴  
Week 5: 성능(병렬성) + DEX 미니 설계 초안  
Week 6: 테스트 자동화 + 보안 리뷰 + 업그레이드 전략  
Week 7: NFT/Metadata + 이벤트 인덱싱(off-chain)  
Week 8: 종합 프로젝트(DAO, Orderbook, Launchpad 중 택1) & Devnet 배포  
Week 9+: 최적화 / Audited 코드 리딩 / Mainnet 릴리즈

---

13. 추천 자료 & 키워드

---

공식 문서: docs.solana.com  
Anchor: book.anchor-lang.com  
Program Examples: github.com/solana-labs/solana-program-library  
Rust: doc.rust-lang.org/book/  
BPF 최적화: “solana bpf limits”, “compute units optimization” 검색  
보안 레퍼런스: Halborn / OtterSec / Neodyme 블로그 (감사 리포트)

---

14. 자주 겪는 시행착오(피트폴)

---

- “계정 space 계산” 잘못 → deserialize panic
- PDA bump 잘못 하드코딩 → future 실패
- writable 과도 지정 → 병렬성 제한
- Anchor test에서 provider.wallet.publicKey()와 실제 signers mismatch
- Devnet에서 insufficient funds (airdrop 실패 반복 → RPC rate limit)
- Token Program CPI에서 owner/signature 누락
- Upgrade authority 잊고 노출된 키로 운영 → 위험

---

15. 다음 액션 추천

---

1. Rust ownership 챕터 복습
2. solana-test-validator 실행 후 간단 counter native 프로그램 배포
3. 동일 기능 Anchor로 재작성
4. PDA 학습: 사용자별 profile 저장
5. SPL Token faucet 만들기(CPI)
6. 코드 리딩: spl-token program entrypoint & processor.rs
7. 이후 내가 도와줄 수 있는 부분:
    - PDA 설계 리뷰
    - 계정 space 계산
    - Anchor 에러/테스트 패턴
    - 성능(동시성) 구조 피드백

---

## 용어 빠른 번역 / Glossary (추가)

- PDA: Program Derived Address / 프로그램 파생 주소
- CPI: Cross Program Invocation / 교차 프로그램 호출
- Rent-exempt: 임대 면제(최소 lamports 보유 상태)
- Compute Units: 실행 연산량 한도 단위
- Instruction: 트랜잭션 내 실행 원자 단위 호출
- Anchor IDL: Interface Definition Language (프론트-백엔드 타입 연동)