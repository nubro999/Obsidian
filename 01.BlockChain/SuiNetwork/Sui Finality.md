Sui Network에서의 Finality는 Mysticeti 합의 메커니즘을 통해 혁신적인 방식으로 구현되며, 블록체인 업계에서 가장 빠른 최종성을 달성합니다.

## Sui의 이중 Finality 시스템

**Fast Path vs Consensus Path**: Sui는 트랜잭션 유형에 따라 두 가지 finality 경로를 제공합니다. 단일 소유 객체(owned object) 트랜잭션은 Mysticeti-FPC를 통한 fast path를 사용하고, 공유 객체(shared object) 트랜잭션은 Mysticeti-C를 통한 일반 합의 경로를 사용합니다.

**Optimistic Finality**: Fast path에서 Sui는 "낙관적 최종성"을 활용하여 충분한 수의 검증자로부터 투표를 받으면 트랜잭션을 즉시 실행합니다. 나중에 무효한 것으로 판명되면 되돌릴 수 있지만, 그 책임은 검증자에게 있습니다.

```
### Sui's Hybrid Transaction Processing Strategy

Sui employs a hybrid strategy for transaction processing. It features a consensus pathway for transactions requiring the agreement of a majority of validators and a "fast path" for transactions that can be executed without consensus. For instance, tasks like "asset transfers, payments, or NFT minting"—described as typical workloads—can be finalized via the fast path before reaching consensus, achieving lower latency.
```
## Mysticeti 합의 메커니즘의 Finality

**즉시 최종성**: 전통적인 블록체인 합의와 달리 Mysticeti는 블록이 구조에 포함되는 즉시 트랜잭션을 최종화합니다. 추가 확인이나 네트워크 활동을 기다릴 필요가 없어 더 빠르고 신뢰할 수 있습니다.

**DAG 기반 커밋**: Mysticeti는 리더가 필요 없는 시스템으로, DAG를 확인하여 블록이 이전 블록으로 링크백한 검증자들의 강한 다수를 가지고 있는지 확인하는 내장 규칙을 통해 블록이 커밋되는 시점을 판단합니다.

## 성능 지표

**Sub-Second Finality**: Sui의 합의 설계는 서브초(sub-second) 최종성을 가능하게 하며, 이는 게임이나 고빈도 DeFi 거래와 같이 속도가 필수적인 애플리케이션에 중요합니다.

**구체적 레이턴시**: 테스트 결과 Mysticeti는 합의에 대해 500밀리초, 단일 소유자 트랜잭션에 대해 250밀리초의 커밋 시간을 보여주며, WAN 환경에서 약 390밀리초의 최종성을 달성합니다.

## 기술적 혁신

**Uncertified DAG Protocol**: Mysticeti는 인증되지 않은 DAG 기반 합의 프로토콜을 활용하여 인증된 DAG 기반 프로토콜과 대비해 레이턴시를 1900ms에서 400ms로 크게 줄였습니다.

**Implicit Commitment**: 전통적인 합의 엔진의 명시적 블록 검증과 인증 대신, Mysticeti는 암시적 커밋을 제공하여 검증자 간 통신을 줄이고 대역폭 사용량을 크게 낮춥니다.

## Effects Certificate System

**최종성 증명**: 트랜잭션 실행 후 검증자들이 독립적으로 트랜잭션의 효과에 서명하여 effects certificate를 형성합니다. 이는 트랜잭션이 수행되고 블록체인에 추가되어 모든 네트워크 참여자에 의해 최종화되었다는 정착 증명입니다.

## 실무적 장점

**일관된 성능**: 리더를 기다리고 투표 라운드를 거칠 필요가 없어 트랜잭션이 더 빠르게 확인되며, 종종 Sui에서 1초 미만으로 처리됩니다. 성능이 더 일관되고 리더 역할의 개별 검증자 성능에 덜 의존적입니다.

**게임 및 실시간 애플리케이션**: Sui의 거의 즉각적인 최종성으로 동적 NFT에 대한 업데이트가 즉시 이루어져 게임이나 실시간 애플리케이션에 이상적입니다.

Sui의 Mysticeti를 통한 finality 시스템은 전통적인 블록체인의 최종성 개념을 혁신하여 업계에서 가장 빠른 합의 레이어로 Sui를 확립했습니다. 이는 차세대 웹3 애플리케이션의 요구사항을 충족하는 핵심 기술적 우위를 제공합니다.