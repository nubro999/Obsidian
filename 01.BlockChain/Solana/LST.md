
1. 용어 정리 (한-영 대응)

- Liquid Staking (유동 스테이킹): SOL을 네트워크 검증(Validator)에 위임(delegation)해 보상을 받으면서, 그 '예치 증표'를 토큰(SPL Token) 형태로 받아 2차 활용(DeFi 등)을 가능케 하는 방식.
- LST (Liquid Staking Token) / LSD(Liquid Staking Derivative): 유동 스테이킹에서 발행되는 파생 토큰 (Solana에서는 일반적으로 SPL 토큰 형태).
- Exchange Rate Model (교환 비율 모델): LST 1개가 시간이 지날수록 더 많은 기본 자산(SOL)에 해당하도록 1 LST : X SOL 비율이 증가하는 구조 (토큰 공급량은 크게 안 변함).
- Rebase Model (리베이스 모델): 토큰 수량 자체가 늘어나며 보상을 반영하는 방식 (Solana 주요 LST들은 대체로 교환 비율 모델 채택).
- Slashing (슬래싱): 검증인 부정행위/이중서명 등 네트워크 합의 위반 시 지분(Stake)의 일부가 삭감되는 처벌.
- Restaking (재스테이킹): 이미 스테이킹된 자산(또는 그 LST)을 추가 보안 서비스 혹은 다른 네트워크/모듈을 보호하는 담보로 다시 활용하여 추가 수익을 창출하는 개념.
- Composability (조합성): 하나의 자산(LST)을 다른 프로토콜(DEX, Lending, Derivatives 등)에서 재사용·중첩할 수 있는 특성.

---

2. Solana 기본 스테이킹 메커니즘 요약

- SOL 스테이킹은 개별 'Stake Account' 단위로 이루어짐 (각 계정은 위임 대상 Validator와 양, 활성/비활성 상태 메타데이터 포함).
- Epoch (에포크) 단위(약 2일 내외)로 보상이 계산되어 Stake Account에 적립.
- Warmup/Cooldown: 활성/비활성 처리에 한 에포크당 네트워크 전체 유효 지분의 일정 비율(대략 25% 수준)까지만 변화 허용 → 대량 이동 급변 리스크 완화.
- 보상 구성: 인플레이션 보상 + 트랜잭션 우선 순위 수수료(priority fees) + MEV(점차 증가 추세) 등이 혼합.

---

3. LST가 해결하는 문제 (1) 기회비용 제거: 전통적 스테이킹은 잠금(Lock)으로 유동성 상실 → LST는 그 '지분 증명 수익 청구권'을 토큰화해 유통 가능. (2) DeFi 조합성: 담보 대출, DEX 유동성 공급, 파생상품(LSDfi) 전략, 구조화 상품 등에 활용. (3) 분산화 향상: 프로토콜이 자동으로 다수의 Validator에 분산 위임함으로써 개별 사용자의 중앙화 선택 편향을 줄임. (4) UX 개선: 직접 Stake Account 생성·Validator 선택·관리 복잡도 완화.

---

4. Solana LST 프로토콜 주요 예시 (프로토콜 현황은 시간이 지남에 따라 변동 가능)

- Marinade (mSOL): 가장 널리 쓰이는 LST 중 하나. 지연 언스테이킹(Delayed Unstake) + 즉시 언스테이킹(유동성 풀 사용, 수수료 존재).
- Jito (JitoSOL): MEV 전략 최적화로 추가 수익 추구. Validator 선정 시 MEV 수익 분배 고려.
- Lido (stSOL): 멀티체인 LST 대표 프로젝트의 Solana 버전 (과거 운영 변경/축소 논의 등 이슈 있었으므로 최신상태 확인 필요).
- BlazeStake (bSOL)
- Socean (scnSOL)
- Sanctum: LST 유동성 라우터/허브(다양한 LST 상호 교환성 및 LST 간 유동성 최적화 지향). (이 외 신생 프로젝트 수시 등장)

각 LST별 차이 포인트:

- Validator 선택 알고리즘: 퍼포먼스 점수, 위임 분산도, 슬래싱 내역, 수수료(commission) 고려.
- 수수료 구조: Validator 커미션 + 프로토콜 수수료(예: 수익 일부 분배).
- 보상 반영 방식: 대부분 Exchange Rate 모델 (예: 시간이 지나면 1 mSOL → 1.01 SOL 가치처럼 비율 증가).
- Unstake 방식: 즉시 언스테이킹(유동성 풀 기반, 스프레드/수수료) vs 지연 언스테이킹(에포크 대기 후 1:1 출금).

---

5. LST 구조 (내부 구성 요소)

6. 사용자 입금 단계:
    - 사용자는 SOL을 LST 프로토콜 스마트 컨트랙트(프로그램)에 예치.
    - 프로그램은 SOL을 여러 Stake Account로 분산 위임(Delegation).
7. 발행 (Mint):
    - 동일 가치의 LST(SPL Token) 발행 후 사용자에게 전송.
    - LST는 보상 발생 시 교환 비율이 점점 높아지는 Claim Token.
8. 보상 반영:
    - Epoch 종료 시 Stake Account에 SOL 보상 적립.
    - 프로토콜은 총 SOL(원금+보상) / 총 LST 발행량 = 새로운 Exchange Rate 계산.
9. 상호 운용:
    - LST는 SPL Token이므로 DEX 풀(예: LST/SOL), Lending 프로토콜 담보, 파생상품 마진 등으로 사용.
10. 언스테이킹:
    - a. 지연(Delayed): 언스테이킹 요청 → Deactivate → Cooldown 후 SOL 수령.
    - b. 즉시(Liquid): 프로토콜 또는 AMM 유동성 풀에서 LST를 SOL과 스왑(가격/슬리피지/수수료).
11. 수수료 & 회계:
    - Validator 커미션이 Stake Reward에서 차감 → 나머지를 Exchange Rate에 반영.
    - 프로토콜 운영 수수료(관리, 보험, DAO 금고 등) 부과 가능.

도식(텍스트): 사용자 SOL → (입금) LST 프로그램 → (위임) 다수 Validator Stake Account → (Epoch 보상) Stake Account 증가 → (Exchange Rate 상승) LST 가치 증가 → (사용자 활용) DeFi 등

---

6. LST 가격/환율 모델 비교

- Exchange Rate Model (Solana 다수): 초기: 1 LST = 1 SOL 시간이 지나며: 1 LST = 1.02 SOL ... (LST 수량 변동 거의 없음, 가치 상승) 장점: 단순, 회계 예측 용이, 복리 시뮬레이션 편리 단점: 초보 사용자에게 직관성 떨어질 수 있음 (LST 가격이 SOL보다 비싸보임)
- Rebase Model (현재 Solana에서 주류 아님): 1 LST 가격은 SOL과 유사, 대신 보상이 발생하면 LST 수량이 증가(에어드롭 비슷) 장점: 1:1 페그 경험 단점: 토큰 수량 변동으로 DeFi 통합 복잡성 증가 (회계 부담)

---

7. LST 활용(Use Cases)

- Lending: LST 담보 대출 → 레버리지 스테이킹 전략 (Looping).
- DEX 유동성: (LST/SOL) 풀에 예치 → 거래 수수료 + IL(Impermanent Loss) 리스크.
- Perps/Derivatives: 마진 자산으로 사용, 금리/커브 기반 구조화 상품.
- Yield Aggregation: 자동 복리 또는 여러 LST 간 스위칭 최적화.
- LSD-Fi(파생 DeFi): LST를 담보로 2차 토큰 발행, 수익 분리(Principal vs Yield 토큰화) 구조.
- Collateral in Bridges or Cross-chain: LST를 래핑해 다른 체인 전송 후 재활용.

---

8. 리스크 분석

9. 스마트 컨트랙트 리스크: 프로토콜 버그, 권한(업그레이드 키) 오남용.
10. Validator 리스크: 집중화, 퍼포먼스 저하(미수령 보상), 슬래싱(현재 Solana에서는 슬래싱 사건 빈도 낮지만 가능성 존재).
11. 유동성 리스크: 즉시 언스테이킹 풀 고갈 시 큰 슬리피지.
12. 페그(가격) 리스크: 시장 공포/강제 청산 시 LST가 내재가치(DISCOUNT) 아래에서 거래.
13. MEV 및 우선순위 수수료 변동: 예상 수익률 변동성 증가.
14. 재스테이킹(추가 담보화) 시: 다중 슬래싱/복합 담보 청구권(Overlapping Claims)으로 시스템 단계적 불안정성 가능.

---

9. Re-Staking(재스테이킹) 개념과 Solana 적용 이슈 (1) 개념:

- 이미 스테이킹되어 기본 네트워크 보안을 제공하는 지분(LST나 Native Staked SOL)을 추가로 다른 서비스(AVS: Actively Validated Service), 예: 오라클 네트워크, 데이터 가용성(DA) 레이어, 경량 롤업, 크로스체인 메시징, 검증 레이어 등에 담보화하여 추가 수익(수수료 / 토큰 인센티브)을 얻는 구조.
- 이더리움 EigenLayer 모델이 대표적 사례 (추가 Slashing 조건 모듈화).

(2) Solana 특수성(제약):

- Solana 기본 레이어 슬래싱 범위 제한: 현재 슬래싱 이벤트가 빈번하지 않으며, 임의 커스텀 조건으로 L1이 바로 지분 삭감하는 구조 아님.
- Stake Account 권한 모델: 재스테이킹 모듈이 '조건부 슬래싱'을 구현하려면 별도 프로그램이 LST 또는 담보로 예치된 SOL을 보유/락업하고, 위반 증명(proof)을 제출받아 자산 몰수/소각하는 2차적 메커니즘을 구현해야 함 (L1 본래 슬래싱과는 별개).
- 높은 TPS와 짧은 확정성(Finality) 덕분에 AVS 수요(예: 오라클, Rollup 시퀀서)가 나올 경우 재스테이킹 경제 논리가 생길 잠재력.

(3) 가능한 설계 패턴: A. LST Escrow + Slash Module:

- 사용자: LST 예치 → rLST(재스테이킹 토큰) 수령
- 모듈: 위반 증명 수신 → rLST 보유자의 담보 비율에 따라 일부 소각 또는 벌금금(예: SOL 준비금) 차감 B. Dual Token Risk Layer:
- 기본 LST 보상 + 재스테이킹 서비스 수익(AVS Fee, 토큰 인센티브) 분리 발행 (예: Principal Token / Yield Token 구조로 추가 파생 가능) C. Insurance Pool 모델:
- 재스테이킹 참여자 일부 수익을 보험 풀에 적립 → 위반/손해 발생 시 보상 D. Modular AVS Registry:
- 레지스트리 프로그램에 각 AVS 등록 → 필요한 최소 담보량, 슬래싱 조건, 모니터/챌린저 역할 정의.

(4) 경제적 논리: 총 기대 수익률 ≈ 기본 스테이킹 수익률(인플레이션+수수료+MEV) + 재스테이킹 인센티브(AVS Fee + 토큰 보조) - 리스크 프리미엄 리스크 프리미엄은 복합 슬래싱 가능성, 유동성 저하, 스마트 컨트랙트 레이어 추가로 증가.

(5) 위험 (Layered Slashing):

- 중첩 담보: 같은 SOL 가치에 대해 L1 보상 청구권 + AVS 담보 청구권이 겹침.
- Tail Risk: 대규모 위반(오라클 조작 등)으로 AVS가 슬래싱 → LST 시장 신뢰 훼손 → 할인 폭 확대 → 대출 청산 연쇄.
- 거버넌스 공격: 재스테이킹 레지스트리 파라미터 변경(슬래싱 임계값 완화/강화)로 이해 상충 가능.

(6) 현 단계(요약):

- Solana 재스테이킹은 개념적·실험적 단계로, Ethereum EigenLayer 수준의 표준화/대규모 모듈 생태계는 아직 미성숙.
- 초기 구현 시 '진짜 L1 슬래싱'이 아니라 '프로그램 내부 경제적 패널티'로 모사하는 형태가 유력.

---

10. Re-Staking 설계 시 핵심 고려 항목 (Solana 관점)

- Stake Authority 관리: 여러 Validator에 분산된 Stake Account의 withdraw/delegate 권한을 멀티시그 또는 프로그램에 위임해 보안 강화.
- Slashing Proof Format: 오라클/서비스 위반 증명 데이터 구조(CPI 호출, 서명 검증, Merkle proof 등).
- Partial vs Socialized Slashing: 위반자 개별 식별이 어려우면 풀 전체 비례 차감(사회화) → 선의 사용자까지 벌금 → 사용자 이탈 리스크.
- Liquidity Layer: rLST(재스테이킹 토큰) 즉시 유동성을 위한 AMM/StablePair 구축.
- Risk Tranching(위험 분리): Senior (원금 우선 보호) / Junior (추가 수익+먼저 피해) 구조로 자본 효율 vs 안정성 균형.
- Oracle Dependencies: 다층 구조에서 오라클 실패는 시스템적 손실 트리거 → 모니터/챌린저 인센티브 설계 중요.

---

11. LST 선택/비교 시 체크리스트

- TVL, 유동성 깊이 (DEX, Lending 마켓 깊이)
- Validator 분산도(Top N 집중 비율)
- 프로토콜 감사(Audit) 보고서 유무, 업그레이드 권한 타임락(Time-lock)
- 언스테이킹 대기 기간 & 즉시 언스테이킹 비용(수수료/슬리피지)
- MEV 최적화 전략 유무(Jito 등)
- 수수료 구조(Validator Commission + Protocol Fee)
- 보험/슬래싱 커버 펀드 존재 여부
- 커뮤니티 거버넌스 투명성

---

12. 간단한 예시 시뮬레이션 (Exchange Rate 방식) 가정:

- 초기: 1 mSOL = 1 SOL
- 1년 후 총 스테이킹 수익률(복합) 8% (슬래싱 없음, 수수료 후) → 1 mSOL 교환 비율: 1.08 SOL 사용자가 100 SOL 예치 → 100 mSOL 발행 → 1년 후 100 mSOL = 108 SOL 가치 (토큰 수량 그대로, 교환 비율만 상승)

만약 재스테이킹 수익 추가(연 3% 가산) → 총 11% → 1 mSOL = 1.11 SOL 그러나 추가 리스크(예: 잠재 슬래싱 기대손실 1%) 고려 실효 기대수익 ≈ 10%

---

13. 요약 핵심 포인트

- LST는 SOL 스테이킹 지분을 토큰화해 유동성과 DeFi 조합성을 제공.
- 구조는 Stake Account 집합 + 발행 SPL 토큰 + 수익률 반영(교환비율) + 언스테이킹(지연/즉시) 모듈.
- Re-staking은 이 지분(혹은 LST)을 다시 다른 보안/서비스 네트워크 담보로 활용해 추가 수익을 얻으려는 차세대 모델.
- Solana에서 재스테이킹은 기술적 제약(L1 슬래싱 한계, Stake Account 모델) 때문에 '내부 경제적 슬래싱' 구현 형태가 될 가능성이 크며 아직 초기.
- 리스크(중첩 슬래싱, 유동성, 거버넌스) 관리가 확산의 핵심.

---

14. 학습/추가 탐구 추천 키워드

- Solana Stake Program
- Marinade Architecture
- Jito MEV & Priority Fees
- Sanctum LST Routing
- EigenLayer (Ethereum) vs Solana Re-staking 가능성 비교
- Risk Tranching in LSD-Fi
- MEV Auction & Validator Client Optimizations

---

15. 빠른 영-한 주요 용어 매핑

- Delegation: 위임
- Stake Account: 스테이크 계정
- Validator Commission: 검증인 수수료
- Epoch Boundary: 에포크 경계
- Exchange Rate: 교환 비율
- Immediate Unstake (Liquid Unstake): 즉시 언스테이킹
- Delayed Unstake: 지연 언스테이킹
- Slashing: 슬래싱(지분 삭감)
- Restaking Module: 재스테이킹 모듈
- AVS (Actively Validated Service): 능동 검증 서비스
- Liquidity Pool: 유동성 풀
- Impermanent Loss: 미실현 손실(IL)
- MEV (Maximal Extractable Value): 최대 추출 가치
- Composability: 조합성
- Escrow: 에스크로(조건부 보관)
- Tranching: 트랜칭(위험 등급 분리)
- Proof Submission: 증명 제출