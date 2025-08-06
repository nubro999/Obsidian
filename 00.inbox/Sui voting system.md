
Sui Network의 투표 시스템은 Delegated Proof-of-Stake(DPoS) 메커니즘을 기반으로 한 정교한 구조로, 여러 계층에서 다양한 형태의 투표가 이루어집니다.

## 핵심 투표 구조

**고정된 총 투표권**: Sui에서 총 투표권은 스테이킹된 양에 관계없이 항상 10,000으로 고정되어 있습니다. 따라서 쿼럼 임계값은 6,667(2/3 이상)입니다 [Dynamic quorum, voting problem with exchange dag 3 node - Microsoft Q&A](https://learn.microsoft.com/en-us/answers/questions/248770/dynamic-quorum-voting-problem-with-exchange-dag-3).

**개별 검증자 투표권 상한**: 각 검증자는 스테이킹 풀의 SUI에 비례한 합의 투표권을 가지지만, 개별 검증자의 투표권은 1,000(전체의 10%)으로 제한됩니다. 검증자가 총 스테이크의 10% 이상을 축적하면 투표권은 10%로 고정되고, 나머지 투표권은 다른 검증자들에게 분배됩니다 [Dynamic quorum, voting problem with exchange dag 3 node - Microsoft Q&A](https://learn.microsoft.com/en-us/answers/questions/248770/dynamic-quorum-voting-problem-with-exchange-dag-3).

## 트랜잭션 처리를 위한 투표 시스템

### 소유 객체(Owned Object) 트랜잭션

소유 객체 트랜잭션의 처리 과정은 다음과 같습니다: [What is Sui Network? (SUI) How it works, who created it and how it is used | Kraken](https://www.kraken.com/learn/what-is-sui-network-sui)

1. **트랜잭션 브로드캐스트**: 발신자가 네트워크의 한 노드에 트랜잭션을 전송하면, 모든 검증자 노드에 브로드캐스트됩니다.
2. **DPoS 투표**: 검증자들이 DPoS(위임된 지분 증명)를 수행하여 받은 트랜잭션의 유효성에 대해 투표합니다. 각 검증자의 투표는 자체 스테이킹 + 위임된 Sui 양에 따라 가중치가 부여됩니다 [What is Sui Network? (SUI) How it works, who created it and how it is used | Kraken](https://www.kraken.com/learn/what-is-sui-network-sui).
3. **인증서 생성**: 클라이언트는 쿼럼만큼의 검증자로부터 서명을 수집하여 인증서를 형성합니다 [SuiNS Governance Voting and Rewards Explained](https://blog.sui.io/suins-governance-voting-rewards/).

### 공유 객체(Shared Object) 트랜잭션

공유 객체 트랜잭션은 더 복잡한 합의 과정을 거칩니다: [What is Sui Network? (SUI) How it works, who created it and how it is used | Kraken](https://www.kraken.com/learn/what-is-sui-network-sui)

1. **Byzantine Consistent Broadcast (BCB)**: 모든 검증자 노드가 동일한 트랜잭션 요청을 받도록 하는 알고리즘이 사용됩니다.
2. **합의 기반 투표**: 순서가 필요한 트랜잭션들은 Mysticeti 합의 엔진을 통해 처리됩니다.

## 실제 투표 메커니즘 예시

### 쿼럼 달성 시나리오

```
총 투표권: 10,000
쿼럼 요구사항: 6,667 (66.7%)

검증자별 투표권 분배:
- 검증자 A: 1,000 (10% 상한)
- 검증자 B: 800 (8%)
- 검증자 C: 1,000 (10% 상한)
- 검증자 D: 600 (6%)
- 나머지 검증자들: 6,600 (66%)

유효한 트랜잭션 인증을 위해서는 최소 6,667의 투표권을 가진 
검증자들의 서명이 필요
```

### 가스 가격 투표 예시

각 검증자는 다음 에포크의 기준 가스 가격에 대한 견적을 제출하는 객체를 소유합니다. 가격을 변경하려면 해당 객체의 값을 업데이트해야 합니다: [In-Depth Analysis of Sui Staking and LSD from a Security Perspective | MoveBit：Pioneer in Move Security | Move Smart Contract Security Audit Service for Aptos and Sui](https://www.movebit.xyz/blog/post/In-Depth-Analysis-of-Sui-Staking-and-LSD-from-a-Security-Perspective.html)

bash

```bash
# 다음 에포크의 가격 견적을 42로 설정하는 예시
$ sui client call \
  --package <PACKAGE-ID> \
  --module sui_system \
  --function request_set_gas_price \
  --args 0x5 "42" \
  --gas-budget <GAS-AMOUNT>
```

## DAG 기반 암시적 투표

**Mysticeti의 혁신**: 전통적인 합의 엔진이 명시적 블록 검증과 인증을 요구하는 반면, Mysticeti는 검증자들이 서명하고 투표를 브로드캐스트하는 통신 오버헤드 대신 암시적 커밋을 제공합니다.

**3라운드 메시지**: DAG에서 블록을 커밋하기 위해 단 3라운드의 메시지만 필요하며, 이는 실용적 비잔틴 장애 허용과 동일하고 이론적 최소값과 일치합니다.

## 거버넌스 투표 시스템

### Tallying Rule 구현

검증자 성능에 대한 사회적 균형을 통해 구현됩니다: [In-Depth Analysis of Sui Staking and LSD from a Security Perspective | MoveBit：Pioneer in Move Security | Move Smart Contract Security Audit Service for Aptos and Sui](https://www.movebit.xyz/blog/post/In-Depth-Analysis-of-Sui-Staking-and-LSD-from-a-Security-Perspective.html)

bash

```bash
# 성능이 좋지 않은 검증자 신고 예시
$ sui client call \
  --package <PACKAGE-ID> \
  --module sui_system \
  --function report_validator \
  --args 0x5 0x44840a79dd5cf1f5efeff1379f5eece04c72db13512a2e31e8750f5176285446 \
  --gas-budget <GAS-AMOUNT>
```

검증자 세트는 자체적으로 모니터링을 수행하고, 한 검증자가 명백히 성능이 좋지 않으면 다른 검증자들이 해당 검증자에게 0점을 주고 보상을 삭감해야 합니다 [In-Depth Analysis of Sui Staking and LSD from a Security Perspective | MoveBit：Pioneer in Move Security | Move Smart Contract Security Audit Service for Aptos and Sui](https://www.movebit.xyz/blog/post/In-Depth-Analysis-of-Sui-Staking-and-LSD-from-a-Security-Perspective.html).

## 보안과 BFT 보장

**2/3 쿼럼의 중요성**: Sui 네트워크는 전체 스테이크의 2/3 쿼럼이 정직한 당사자들에게 할당되어 있는 한 보안 속성을 유지합니다.

**인증서 정책**: 인증서만을 커밋하는 정책은 비잔틴 장애 허용을 보장합니다. 검증자의 2/3 이상이 프로토콜을 충실히 따르면 커밋된 인증서 세트와 그 효과에 대해 결국 합의에 도달할 것이 보장됩니다 [SuiNS Governance Voting and Rewards Explained](https://blog.sui.io/suins-governance-voting-rewards/).

이러한 다층적 투표 시스템은 Sui Network가 높은 처리량과 낮은 지연시간을 유지하면서도 강력한 보안과 탈중앙화를 달성할 수 있게 하는 핵심 메커니즘입니다.