
# 쿠버네틱스(Kubernetes)란?

# 1. Kubernetes의 철학: 선언형(Declarative) + 지속적 조정(Reconciliation)

- 당신(사용자)은 “현재 어떻게 되어 있는지”를 직접 명령하지 않고, “원하는 상태(Desired State)”만 선언(YAML 등)합니다.
- Kubernetes는 “실제 상태(Actual / Current State)”를 계속 관측(Watch)하며 원하는 상태와 다르면 “조정(Reconcile)”하는 **컨트롤 루프(Control Loop)** 구조로 작동합니다.
- 핵심 개념:
    1. 선언형 상태 저장: etcd (분산 Key-Value Store)
    2. API Server: 단일 진입점 및 상태 변경의 관문
    3. Controller/Scheduler: 상태 비교 → 조정 행위 실행
    4. Kubelet: 노드 단에서 실제 컨테이너 실행/상태 보고

이 패턴은 GitOps, 인프라 불변성, 자동 복구(Self-healing) 같은 상위 개념으로 확장됩니다.

---

# 2. 아키텍처 개요

## 2.1 Control Plane (제어 평면)

|컴포넌트|역할 (Korean 설명)|
|---|---|
|kube-apiserver|모든 요청의 게이트웨이 (인증/인가/검증/변환). 클라이언트와 내부 컴포넌트가 전부 여기와만 대화|
|etcd|클러스터 “단일 진실 소스(Single Source of Truth)” 분산 저장소 (Raft 합의)|
|kube-scheduler|새로 생성(할당 전)된 Pod를 어떤 노드에 배치할지 결정 (Filter + Score)|
|controller-manager|다양한 Controller 실행(ReplicaSet, Deployment, Node, Endpoint, Job 등) – 각 컨트롤 루프 집합|
|cloud-controller-manager (선택)|Cloud Provider 의 LoadBalancer, Node, Route, Volume 연계 로직 분리|

## 2.2 Node (작업자 노드)

| 컴포넌트                    | 역할                                                     |
| ----------------------- | ------------------------------------------------------ |
| kubelet                 | PodSpec 수신 → 컨테이너 런타임 호출 → 상태 보고 → Probe 실행            |
| kube-proxy              | Service 가상 IP → 실제 Pod IP로 트래픽 전달 (iptables/IPVS/eBPF) |
| Container Runtime (CRI) | containerd, CRI-O 등. 실제 이미지 Pull, 컨테이너 생성 (runc 호출)    |
| cAdvisor(내장)            | 리소스 사용량 메트릭 수집 (kubelet 통해 노출)                         |

---

# 3. 리소스 모델과 오브젝트 (K8s Objects)

Kubernetes는 “상태를 정의하는 문서”를 오브젝트로 저장합니다.

주요 오브젝트:

- Namespace: 논리적 격리
- Pod: 스케줄링의 최소 배치 단위(하나 이상의 컨테이너 + 공유 네트워크/볼륨)
- ReplicaSet: 특정 Pod 템플릿의 복제 개수 유지
- Deployment: ReplicaSet 롤링 업데이트/롤백 관리 상위 추상화
- StatefulSet: 상태 있는 Pod(순서, 안정된 네트워크 ID, PersistentVolumeClaim) 관리
- DaemonSet: 모든(또는 일부) 노드마다 1개 Pod 보장 (예: 로그 수집, 모니터링 에이전트)
- Job / CronJob: 일회성 / 주기성 작업
- Service: Pod 집합에 대한 안정된 네트워크 접근(ClusterIP, NodePort, LoadBalancer)
- Ingress: 7계층 HTTP(S) 라우팅 (Ingress Controller 필요, Nginx, Traefik 등)
- ConfigMap / Secret: 설정/민감 데이터 분리 (환경변수/파일 마운트)
- ServiceAccount / RBAC: 권한/토큰 기반 인증/인가
- PersistentVolume (PV) / PersistentVolumeClaim (PVC): 스토리지 추상화 (CSI 드라이버 통해 외부 스토리지 연동)
- NetworkPolicy: Pod 간 트래픽 허용/차단 규칙

---

# 4. 동작 흐름 (Pod 생성에서 실행까지)

1. 사용자가 Deployment YAML 적용 (kubectl apply → kube-apiserver)
2. API Server는 유효성 검증 + Admission(변환/정책) → etcd에 저장
3. ReplicaSet Controller: etcd watch → 원하는 replica 수 vs 현재 pod 수 비교 → 부족하면 Pod 객체 생성
4. 새 Pod 객체는 아직 Node가 할당되지 않은 상태 (spec.nodeName 없음)
5. Scheduler: API Server에서 “할당 전” Pod 목록 watch → 스케줄링 (Filter + Score) → Bind 요청(어떤 노드 선택)
6. kubelet(해당 노드): 자신에게 bind된 PodSpec watch → 컨테이너 런타임 호출 → 이미지 pull → 컨테이너 생성
7. CNI 플러그인 호출: Pod 네트워크 네임스페이스 생성, IP 할당
8. kubelet: readiness/liveness/startup probe 감시, 상태 업데이트 (Pod Status)
9. Service/Endpoints Controller: 레이블 셀렉터로 Pod IP 목록 갱신 → kube-proxy 갱신 (iptables/IPVS)
10. 클라이언트/다른 Pod가 Service IP로 접근 → kube-proxy/라우팅을 통해 실제 Pod로 전달

---

# 5. Watch & Reconciliation 메커니즘

- API Server는 etcd 변경을 기반으로 “리소스 버전(resourceVersion)” 제공.
- Controller/Scheduler/kubectl 등 클라이언트는 List → Watch 스트림을 구독.
- 변경 이벤트(ADDED, MODIFIED, DELETED)를 수신하면 내부 큐에 넣고, 조정(Reconcile) 실행.
- 네트워크 장애/Watch 끊김 → 재연결(List + resourceVersion 재동기화).
- 결국 “Pull”이 아니라 “지속적 리스트-워치 기반의 이벤트 드리븐” 패턴.

---

# 6. 스케줄러 원리 (간단 알고리즘 흐름)

1. Pending Pod 후보 선택 (FIFO 큐 또는 플러그인 전략)
2. Filter 단계: Node 리소스 여유, Taint/Toleration, NodeSelector/NodeAffinity, PodAffinity/AntiAffinity, 포트 충돌, Volume 접근 가능성 등
3. Score 단계: 남은 CPU/메모리 균형, Topology Spread, PreferredAffinity, Custom 플러그인 점수
4. 최종 Node 선택 → Bind API 호출 → Pod spec.nodeName 세팅
5. Extensible: Scheduling Framework 플러그인(PreFilter, Filter, Score, Reserve, Permit, Bind 등)

---

# 7. 네트워킹 모델 (CNI 기반)

핵심 가정:

- 모든 Pod는 클러스터 내부에서 “고유한 IP”를 가지며, NAT 없이 서로 직접 통신 가능 (Pod-to-Pod Flat Network) 구성 요소:
- CNI Plugin (Calico, Flannel, Cilium, Weave Net 등):
    - Pod 네임스페이스 생성 시 실행 → veth 페어, 브리지/라우팅/eBPF 엔트리 설정
- Service 구현:
    - ClusterIP: 가상 IP (kube-proxy가 iptables/IPVS/eBPF 룰로 DNAT)
    - NodePort: 각 노드 특정 포트 오픈 → 요청을 해당 Service로
    - LoadBalancer: Cloud Provider 연동 → 외부 LB → NodePort → Pod
    - Headless Service (clusterIP: None): DNS 기반 Pod 목록 직접 반환 (StatefulSet 접두사 명명 활용)
- Ingress:
    - Ingress Controller (예: Nginx) 내부적으로 Service/LB와 연계 → HTTP Host/Path 기반 라우팅
- NetworkPolicy:
    - CNI가 네트워크 정책을 지원해야 동작 (Calico/Cilium 등)
    - 기본 Deny 설정 후 필요한 Allowed Ingress/Egress 지정

신기술:

- eBPF 기반 (Cilium): kube-proxy 대체, 더 빠른 Service 로드밸런싱/네트워크 정책

---

# 8. 스토리지 및 볼륨

- 컨테이너 자체는 Stateless → 상태 유지 필요 시 볼륨
- Volume 종류: emptyDir(노드 임시), hostPath(로컬 디렉토리), PersistentVolumeClaim(동적 프로비저닝)
- CSI(Container Storage Interface):
    - 스토리지 벤더 → CSI 드라이버 → 동적 프로비저닝 (StorageClass)
- StatefulSet:
    - stable identity + 순서 보장 + Pod 마다 PVC 바인딩 (volumeClaimTemplates)

---

# 9. 보안 (Security)

- Authentication: X.509 인증서, Bearer Token, OIDC, ServiceAccount 토큰
- Authorization: RBAC(Role/ClusterRole + RoleBinding/ClusterRoleBinding)
- Admission Controllers:
    - Mutating: 객체 수정 (예: 사이드카 주입 – Istio)
    - Validating: 정책 강제(Opa/Gatekeeper, Pod Security Admission)
- Pod Security (기존 PodSecurityPolicy 폐지): baseline / restricted 프로파일
- 네임스페이스 격리 + NetworkPolicy + ResourceQuota + LimitRange 조합
- Secret:
    - etcd 내 base64 저장(기본 암호화 X) → at-rest encryption 설정 권장
- 컨테이너 런타임 샌드박스: seccomp, AppArmor, SELinux, rootless 컨테이너

---

# 10. 리소스/성능/스케줄링 OS 관점 연결

컨테이너 내부 동작은 Linux 커널 기능을 재활용:

- Namespace: pid, net, mnt, uts, ipc, user → 격리
- cgroups: CPU shares, CPU quota, memory limit, blkio, pids 제한
- OverlayFS: 레이어드 이미지 (Copy-on-Write)
- kubelet은 PodSpec의 requests/limits → cgroups 구성 → OOM 발생 시 커널 OOM Killer 작동 → kubelet이 Pod 재시작 가능 QoS Class:
- Guaranteed: requests == limits (CPU/Memory 모두)
- Burstable: 일부만 일치
- BestEffort: requests/limits 없음 → 가장 먼저 축출(evict) 대상

Eviction:

- 노드 메모리 압박 → kubelet이 Pod을 종료(Evict), 우선순위: BestEffort → Burstable → …
- PriorityClass: 높은 우선순위 Pod는 낮은 우선순위 Pod 축출하여 자리 확보 가능(Preemption)

---

# 11. 헬스 체크 & 자기치유(Self-Healing)

- Liveness Probe: 실패 시 컨테이너 재시작
- Readiness Probe: 실패 시 Service Endpoints에서 제외 (트래픽 차단)
- Startup Probe: 애플리케이션 초기 부팅 오래 걸릴 때 liveness 지연 완화
- Controller:
    - ReplicaSet: 실제 Pod 수 != 목표 replicas → 생성/삭제
    - Node Controller: 노드 Heartbeat 끊기면 NotReady → 일정시간 후 Pod 이전(taint + eviction)

---

# 12. 롤링 업데이트 & 배포 전략

Deployment:

- RollingUpdate: maxSurge, maxUnavailable 파라미터로 점진적 교체
- Rollback: 이전 ReplicaSet 기록 → kubectl rollout undo 고급 패턴:
- Blue/Green: 두 버전 병행 배치 → Service 전환
- Canary: 소수 트래픽만 새 버전 → 점진 확장 (Ingress Controller, Service Mesh 라우팅)
- Progressive Delivery: 자동 메트릭 평가(HPA + Argo Rollouts)

---

# 13. 오토스케일링

- HPA(Horizontal Pod Autoscaler): CPU/메모리/Custom Metrics 기반 replicas 조정
- VPA(Vertical Pod Autoscaler): requests/limits 자동 추천/조정 (재시작 필요)
- Cluster Autoscaler: 노드 규모 자동 조정 (클라우드 Provider API 호출)
- PodDisruptionBudget(PDB): 자발적 중단(업데이트/노드 스케일 인) 시 최소 가용성 보장

---

# 14. Observability (가시성)

- Metrics: kubelet/cAdvisor + Metrics Server (HPA 활용) + Prometheus (커스텀)
- Logging: stdout/stderr → node 로그 수집(Fluent Bit/Fluentd/Vector) → ES/OpenSearch
- Tracing: OpenTelemetry + sidecar/agent → Jaeger/Tempo
- Events: kubectl describe 로 객체 이벤트 확인 (스케줄링 실패, Pull 실패 등)
- Debugging:
    - kubectl exec / logs / cp / port-forward
    - Ephemeral Containers (디버깅용 주입)

---

# 15. 확장성 생태계 인터페이스

- CRD(CustomResourceDefinition): 사용자 정의 리소스 추가 → Controller(Operator 패턴)로 도메인 자동화
- Operator: CRD + 컨트롤 루프 → 복잡한 상태풀 시스템 관리 (예: DB 클러스터)
- CSI: 스토리지 표준화
- CNI: 네트워크 플러그인 표준화
- CRI: 컨테이너 런타임 표준화
- Admission Webhook: 동적 정책 주입/검증
- API Aggregation: 확장 API 서버 조합 가능

---

# 16. etcd 내부 원리 간단 개요

- 분산 합의 알고리즘: Raft
- 모든 Control Plane 컴포넌트는 읽기/쓰기 API Server 경유 → etcd 일관성 유지
- Watch: Key prefix 기반 변경 스트림 제공 → K8s Controller가 효율적 이벤트 처리
- 성능 고려:
    - Write 집중 시 디스크/네트워크 지연 → API Server 슬로우
    - 압축(compaction), defragment 필요

---

# 17. 장애 복구 / 탄력성

- Pod Crash: kubelet + Controller 자동 재생성
- Node Down: Node Controller → taint → Pod 재스케줄
- Control Plane 장애:
    - Multi-Master HA (API Server + etcd 다중화)
    - etcd 백업/복구 전략 중요 (주기적 snapshot)
- 데이터 손실 대응:
    - 중요한 Secret/PV 외부 백업
    - GitOps (Argo CD)로 선언형 소스 회복

---

# 18. 선언형 vs 명령형 (Imperative)

- 명령형: kubectl run ... / create deployment ... (즉시 동작)
- 선언형: kubectl apply -f manifest.yaml (상태 정의 중심, diff & patch)
- GitOps: Git 저장소 = 선언적 소스; 컨트롤러가 주기적 동기화

---

# 19. 실제 YAML 예시 (설명 주석 포함)

복사

`apiVersion: apps/v1 kind: Deployment metadata:   name: demo-api   labels:     app: demo-api spec:   replicas: 3                    # 원하는 상태(3개 Pod)   selector:     matchLabels:       app: demo-api   strategy:     type: RollingUpdate     rollingUpdate:       maxSurge: 1                # 추가로 1개 더 만들 수 있음       maxUnavailable: 1          # 동시에 1개까지 비활성 가능   template:     metadata:       labels:         app: demo-api     spec:       containers:         - name: api           image: myrepo/demo-api:1.2.3           resources:             requests:               cpu: "100m"               memory: "128Mi"             limits:               cpu: "300m"               memory: "256Mi"           ports:             - containerPort: 8080           readinessProbe:             httpGet:               path: /healthz               port: 8080             initialDelaySeconds: 5             periodSeconds: 10           livenessProbe:             httpGet:               path: /live               port: 8080             initialDelaySeconds: 15             periodSeconds: 20 --- apiVersion: v1 kind: Service metadata:   name: demo-api-svc spec:   selector:     app: demo-api   type: ClusterIP   ports:     - port: 80          # 클러스터 내 서비스 포트       targetPort: 8080  # Pod 컨테이너 포트`

---

# 20. Kubernetes가 제공하는 “가치” 요약

- 추상화: 인프라 → “상태”만 선언
- 자가치유: 컨테이너/노드 장애 자동 대응
- 확장성: 수평/수직/클러스터 자동 조정
- 이식성: 클라우드/온프렘 동일한 API
- 확장 가능: CRD/Operator/Plugin Eco
- 보안/정책/멀티테넌시 지원

---

# 21. 학습/이해를 위한 추천 흐름

1. Linux 컨테이너 기본 (namespace, cgroups, overlayfs)
2. kubectl로 Pod/Deployment/Service 실험
3. Probe, Resource Requests/Limits 적용 → OOM/Evict 관찰
4. ConfigMap/Secret → 환경분리
5. HPA + 부하테스트
6. NetworkPolicy 적용 → 허용/차단 검증
7. StatefulSet + PVC + CSI 스토리지
8. CRD/Operator 예제 (예: cert-manager, Prometheus Operator)
9. GitOps(Argo CD) + Observability Stack(Prometheus, Grafana)

---

# 22. 자주 혼동되는 개념 정리 (요약)

- Pod vs Container: Pod는 하나 이상의 컨테이너 + 공유 리소스(IPC/Net/Vol)
- ReplicaSet vs Deployment: Deployment는 롤링 업데이트 전략/히스토리 관리
- Service vs Ingress: Service는 L4 추상화, Ingress는 L7 HTTP 라우팅
- Request vs Limit: 스케줄링(배치) 기준 vs 런타임 상한선
- Liveness vs Readiness: 살아있는지 vs 트래픽 받을 준비됐는지

---

# 23. 내부 심화 질문 아이디어 (학습 체크)

- 왜 kube-apiserver가 단일 관문이어야 하는가? (일관성/보안/감사)
- etcd write 성능이 떨어지면 어떤 증상이 나오는가?
- 스케줄러 Filter 단계에서 PodAffinity와 NodeSelector 차이?
- kube-proxy iptables vs IPVS vs eBPF 비교?
- HPA가 Custom Metrics 사용할 때 흐름은?
- StatefulSet이 Deployment로 대체될 수 없는 이유는?

---

# 24. 추가로 더 깊게 파고 싶을 수 있는 주제

- Scheduler Framework Plugin 개발
- Controller Runtime(Operator SDK) 내부 큐 동작
- Admission Webhook 최적화와 성능
- eBPF 기반 Service 가속(Cilium)
- Multi-Cluster / Federation / Service Mesh (Istio)
- WASM 런타임(Krustlet) 실험
- Node Feature Discovery + Topology Aware Scheduling

---

# 25. 요약(한 줄)

Kubernetes는 etcd에 선언된 “원하는 상태”를 다수의 분산 컨트롤 루프가 지속 감시·조정하여, 애플리케이션을 탄력적·확장 가능·자가치유 가능한 형태로 실행하도록 하는 모듈식 오케스트레이션 플랫폼입니다.

---

더 궁금한 세부 영역(예: 스케줄러 내부 플러그인, 네트워크 정책 동작 흐름, CSI, Operator 제작 방법 등)을 지정해 주시면 그 부분만 깊게 파서 설명해 드릴게요. 어떤 부분부터 더 파고 싶으세요?


kubernetes소스를 사용하여 컴퓨터리소스를 제공하는 클라우드 컴퓨팅 프로젝트.
suinetwork에서 온체인으로 중개하며, 스테이킹 형식으로 보증을 받음.
walrus에 코드를 올리며, 이를 리소스 제공자는 자신의 컴퓨터(노드)에서 실행을 시킴.
로드밸런서는 kubernetes의 기능을 사용함
npm을 위주로 작동하는 것이 목표


모진영 : 쿠버의 워커노드를 제공자컴퓨터에 구현

신형섭 : 사용자 - 온체인 - 제공자까지의 메커니즘을 만든다. seal로 접근제어

김경훈 : git - wallas 구현해보기

영민 : 프런트, cicd


[[컨테이너 어플리케이션]]