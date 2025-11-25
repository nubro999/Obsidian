 You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs.
 
Kubernetes lets you store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys.

**Batch execution**

선언적 API를 이해하기 위해서는 흔히 사용되는 **명령적 API (Imperative API)**와의 차이점을 아는 것이 중요합니다.

| **구분** | **명령적 API (Imperative)**         | **선언적 API (Declarative)** |
| ------ | -------------------------------- | ------------------------- |
| **방식** | **어떻게(How) 해야 하는지** 지시           | **무엇(What)을 원하는지** 선언     |
| **초점** | **과정(Process)** 및 **단계(Steps)**  | **최종 상태(Desired State)**  |
| **예시** | * "파드 3개를 만들어." → * "파드 2개로 줄여." | * "파드는 항상 3개여야 해."        |
| **도구** | Bash 스크립트, 프로그래밍 언어의 함수 호출       | YAML, JSON 파일             |
|        |                                  |                           |
hub-and-spoke api pattern

[Konnectivity service](https://kubernetes.io/docs/concepts/architecture/control-plane-node-communication/#konnectivity-service)

- Docker는 컨테이너를 생성, 관리하고 개발 생태계를 구축하는 데 필요한 모든 것을 갖춘 자동차와 같습니다.
    
- containerd는 컨테이너를 실제로 움직이게 하는 핵심적인 "엔진"과 같습니다.

다중/분산 쿠버네티스 클러스터 추천


| **구분**                   | **설명**                                                                             | **GPU 렌탈 서비스 적합성**              |
| ------------------------ | ---------------------------------------------------------------------------------- | ------------------------------- |
| **개별 클러스터**              | 각 데이터센터(DC)에 하나의 독립적인 쿠버네티스 클러스터를 구축합니다. 각 클러스터는 해당 DC의 GPU 노드를 관리합니다.             | **필수:** 지역적 독립성 및 낮은 지연 시간 보장.  |
| **상위 레벨 컨트롤러**           | **외부 시스템** 또는 **멀티 클러스터 관리 솔루션** (예: Kubefed, Karmada, Rancher 등)을 사용하여 다음을 수행합니다. | **권장:** 중앙에서 사용자 요청 처리 및 자원 할당. |
| **GPU 렌탈 컨트롤러 (사용자 정의)** | 사용자 정의 컨트롤러(CRD 기반)를 외부에 배치하거나 전용 관리 클러스터에 배치하여 **예약/청구/자원 격리** 등의 비즈니스 로직을 처리합니다. | **필수:** 핵심 서비스 로직 구현.           |
|                          |                                                                                    |                                 |

CRD 기반 클러스터는 사용자 정의 리소스와 컨트롤러를 클러스터에 통합하여 쿠버네티스를 특정 목적에 맞게 '운영체제처럼' 사용하는 클러스터

분산 시스템에서는 공유 자원을 잠그고 집합 구성원 간의 활동을 조정하는 메커니즘을 제공하는 리스(lease)가 종종 필요합니다. 쿠버네티스에서는 리스 개념이 coordination.k8s.io API 그룹의 Lease 객체로 구현되며, 노드 하트비트 및 구성 요소 수준 리더 선출과 같은 시스템 핵심 기능에 사용됩니다.

![[Pasted image 20251119151853.png]]

데이터센터 쿠버네티스 구조 분석 필요

