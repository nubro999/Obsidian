
컴퓨터공학 전공 과정을 이수하며 운영체제, 네트워크, 자료구조, 데이터베이스 등 핵심 개념을 체계적으로 학습했고, MVC 아키텍처 기반의 사이드 프로젝트들을 직접 설계하면서 Web2 환경에서 서비스 구조화와 배포, 유지보수 경험을 쌓았습니다.  
비트코인 백서를 처음 정독했을 때 ‘탈중앙화된 신뢰(trustless consensus)’가 수학적으로 성립한다는 사실이 큰 충격이었고, 이후 블록체인 생태계의 합의/확장성/암호학(머클트리, UTXO 모델, L2 롤업, zk-SNARKs) 관련 개념을 스스로 리서치하며 이해한 내용을 꾸준히 위키 형태로 기록하고 있습니다.

Mina 체인에서 zk-SNARKs 기반 NFT 경매 웹 애플리케이션 ‘SilentAuction’ 프로젝트의 프론트엔드를 담당하며,

- 온체인과 오프체인 증명(Proof) 흐름이 어떻게 UI 상호작용과 연결되는지,
- 사용자 경험(지연·검증 대기)을 최소화하기 위한 비동기 처리/로딩 전략,  
    를 직접 설계·적용해 블록체인 UX 차별점을 체감했습니다.

이후 연세대학교 블록체인 학회(Block Chain at Yonsei)에 참여해 Sui, Ethereum, Solana 등 서로 다른 체인의 객체 모델, 계정 모델, 트랜잭션 처리 차이를 비교 학습하며 소규모 실습 프로젝트를 진행하고 있습니다. 주요 실습으로는

- Solidity를 이용한 Uniswap 스타일 DEX 풀 생성 및 유동성 예치·스왑 트랜잭션 실행,
- Move 언어(Object 모델)를 활용한 실시간 멀티플레이 게임 프로토타입을 Sui 네트워크에 구현하여 BlockBlock Hackathon에 출품

Web3 보안에도 관심이 커 PicoCTF, DreamHack 플랫폼의 문제를 풀며

- 재진입(Reentrancy), 정수 오버플로/언더플로, 접근 제어 미스컨피그, 서명 위조(ECDSA), rawtranstaction 분석
    같은 패턴을 실습했고, 문제 풀이 후 취약점 재현과 패치 방법을 자체 리포트 템플릿에 문서화했습니다. 주 1~2회 이상 지속 학습 사이클을 유지하고 있습니다.

이러한 경험을 통해 리서치 → 실습 → 기록 → 리팩토링과 같은 반복 루프가 제 학습 효율을 가장 높인다는 것을 확인했고, 이를 Web3 제품 및 보안 영역 양쪽에 적용 중입니다.

### (영문 정리 버전)

While completing my Computer Science curriculum, I built a solid foundation in operating systems, networks, data structures, and databases, and reinforced it through MVC-based side projects that taught me practical Web2 service architecture, deployment, and maintenance.  
Reading the Bitcoin whitepaper was a turning point—understanding that decentralized trust can be mathematically guaranteed led me to self-directed research on consensus models, scalability techniques, Merkle trees, UTXO vs. account models, zk-SNARKs, and L2 rollups. I maintain structured notes and an internal wiki to reinforce long-term retention.

In the zk-SNARKs–driven NFT auction project “SilentAuction” on the Mina chain, I owned the frontend implementation and designed the interaction flow between off-chain proof generation and on-chain verification, optimizing asynchronous UX to reduce perceived latency.

Through the Blockchain at Yonsei club, I compared ecosystems across Sui, Ethereum, and Solana—studying differences in object vs. account models, transaction semantics, and developer tooling—while building small experimental projects. Hands-on work includes:

- Recreating core Uniswap flows (pool creation, liquidity provision, swap) in Solidity.
- Implementing a real-time multiplayer game prototype on Sui using the object model and submitting it to [Hackathon name / year], stress-tested locally to ~[X] concurrent simulated players.

My growing interest in Web3 security led me to regularly solve challenges on PicoCTF and DreamHack (≈[N] problems so far), focusing on reentrancy, integer arithmetic vulnerabilities, access control flaws, and signature forgery. For each challenge, I produce a short internal post-mortem with exploitation steps and secure patterns.

These iterative cycles—research → implementation → documentation → refactoring—have become my core learning engine across both decentralized application development and security analysis.

---

## 2. 문항 2

### Share your motivation in applying for Protocol Camp.

### (보강된 한국어 버전)

프로토콜캠프는 단기간(intensive) 안에 실제 ‘프로덕션 수준’ 결과물을 설계·구현·배포까지 경험할 수 있는 구조라는 점에서 제가 원하는 환경과 정확히 맞닿아 있습니다. 올해 졸업 후 정식 취업 전까지 제 역량을 구조적으로 재정비하는 기간에서 프로토콜캠프를 최적으로 활용하고자 합니다.

특히 모든 협업을 영어로 진행하는 점은 제가 지향하는 글로벌 커리어 목표와 직결됩니다. 기술적 의사결정, 코드 리뷰 피드백, 아키텍처 논의를 영어로 수행하는 반복 경험은 향후 국제 해커톤이나 다국적 팀 근무에 핵심 자산이 될 것이라 확신합니다.

또한 “블록체인 학습은 다양한 시야 교차와 실험이 필수”라는 저의 학습 철학과도 부합합니다. 다양한 백그라운드의 참가자들과

- 서로 다른 체인/도구 선택 이유,
- 보안·토큰·거버넌스 설계 트레이드오프,
- 사용자 온보딩/UX 패턴  
    을 논의하며 제 추상적 이해를 구체적 설계 패턴으로 전환하고 싶습니다.

캠프 기간 동안 개인적으로 다음의 내용을 달성하는 것을 목표로 합니다

1. 실사용 가능한 dApp / 프로토콜 1개 이상 End-to-End 배포
2. 내부 또는 자가 Smart Contract 1회 이상 보안 리뷰(Audit-lite) 문서화
3. 기술 블로그/노트 영어 포스팅
4. Mentor 피드백 기반 아키텍처 리팩토링 

이러한 ‘명시적 산출물(Objective)’을 통해 저의 강·약점을 정량화하고, 이후 진로 결정을 위한 실험 데이터를 확보하고자 합니다.

---

## 3. 문항 3

### Share your future goals and visions regarding your career in blockchain.

### (보강된 한국어 버전)

저는 Web3 영역에 지속적으로 남아 기여하고 싶습니다. 현재 제 진로 후보는 (1) 보안 중심(스마트 컨트랙트 감사·오펜시브 테스트)과 (2) 프로덕트/프로토콜 개발 중심(소셜·게임·컨슈머 앱을 통한 생태계 확장) 두 갈래로 열려 있습니다. 불확실성을 단점이 아니라 ‘탐색 단계’로 정의하고, 검증 가능한 실험과 멘토 피드백을 통해 구조적으로 결정을 내릴 계획입니다.

프로덕트/프로토콜 개발 트랙을 선택할 경우:

- ‘금융 편중’을 넘어 실사용 유틸리티(게임 내 자산 상호 운용, 소셜 그래프 서명/평판, 창작자 보상 구조) 영역을 확장하는 서비스를 설계
- 온체인/오프체인 경계(데이터 가용성, 인덱싱, 메시징)를 효율적으로 조정하는 하이브리드 아키텍처 패턴 정립
- 멀티체인 상호운용(브리지 위험 모델 포함)과 사용자 경험 단순화(지갑 추상화, 가스 스폰서) 연구  
    를 통해 보다 넓은 사용자군이 ‘블록체인’을 의식하지 않고 활용하도록 만드는 것을 목표로 합니다.

보안 트랙을 선택할 경우:

- EVM & Move & Rust 기반 컨트랙트 공격면(Attack surface) 체계 분류
- 재진입·프런트러닝·가격 조작·서명 위조·스토리지 레이아웃 충돌 등 취약점 패턴의 표준화된 체크리스트화
- 형식 검증(Formal verification, 예: SMT / 기호 실행) 도구 활용 역량 확보
- 잠재적 Zero-day를 사전에 식별하기 위한 Fuzzing + Differential Testing 파이프라인 구축  
    을 중기 목표로 설정하고 있습니다.


장기적으로는 두 영역이 상호 보완된다고 봅니다. 강건한 보안 판단 능력은 프로덕트 실험 속도를 높이고, 실제 사용자 문제를 해결하는 제품 감각은 보안 리뷰 시 “현실적 위협” 우선순위를 제대로 잡게 합니다.  
최종적으로는:

- 오픈소스 레퍼런스 구현(라이브러리/템플릿) 기여
- 학습 자료(한국어↔영어) 이중화 번역/정리
- Hackathon / Audit 레포트 공개로 커뮤니티 지식 레벨 상승에 기여  
    하는 ‘지식-제품-보안’ 삼각 구조에서 교차 점을 가지는 엔지니어가 되는 것이 제 비전입니다.


---

## 5. 빠른 체크리스트

|항목|포함 여부|개선 여지|
|---|---|---|
|기초 CS 역량|포함|OS/네트워크 구체 과목명/프로젝트 추가 가능|
|블록체인 첫 동기|포함|첫 노트 링크/스크린샷 언급 가능|
|zk-SNARK 실전 경험|포함|사용 라이브러리/Proof 생성 시간 등 수치|
|다중 체인 학습|포함|비교 인사이트 1~2줄 추가 가능|
|Sui 실시간 게임|포함|TPS, latency, 동시 사용자 수치|
|보안/CTF|포함|누적 문제 수, 대표 취약점 패턴 정량화|
|캠프 동기|포함|협업 도구/기대 멘토링 내용 추가 가능|
|목표 KPI|포함|구체 숫자(M, X, N) 채우기|
|진로 탐색 플랜|포함|의사결정 타임라인(예: 캠프 종료 전 2주)에 표기|
|장기 비전|포함|오픈소스 구체 Repo 목표 추가 가능|

---

## 6. 다음 액션 제안

1. 위 초안에서 대괄호 [ ] 부분 수치/링크 채우기
2. 한/영 최종 교차 검수 (용어 일관성: reentrancy ↔ 재진입, frontrunning ↔ 프런트러닝)
3. 분량 제한 있다면 우선순위: 경험 → 동기 → 목표 (임팩트 키워드 유지)
4. 제출 전 Grammarly / 한국어 맞춤법 검사 한 번 (영어·한국어 모두 품질 상승)

---

필요하시면:

- “SilentAuction” 세부 기술 스택 정리 템플릿
- Sui 실시간 게임 성능 측정 문단 샘플
- CTF 리포트 템플릿  
    도 추가 제작해 드릴 수 있습니다.

더 요청 주시면 바로 도와드릴게요!