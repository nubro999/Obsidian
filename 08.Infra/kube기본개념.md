**
Control Plane (마스터 노드)**

- **API Server**: 모든 요청의 진입점, kubectl 명령어가 여기로 전달됩니다
- **etcd**: 클러스터의 모든 상태 정보를 저장하는 분산 key-value 저장소
- **Scheduler**: 새로운 Pod를 어느 노드에 배치할지 결정
- **Controller Manager**: 클러스터의 상태를 지속적으로 모니터링하고 원하는 상태로 유지

**Worker Node**

- **kubelet**: 각 노드에서 실행되며 Pod의 생명주기 관리
- **kube-proxy**: 네트워크 규칙 관리 및 서비스 간 통신 처리
- **Container Runtime**: 실제 컨테이너를 실행 (Docker, containerd 등)

**핵심 리소스**

- **Pod**: 가장 작은 배포 단위, 하나 이상의 컨테이너를 포함
- **Deployment**: Pod의 복제본 관리, 롤링 업데이트
- **Service**: Pod 그룹에 대한 네트워크 엔드포인트 제공
- **ConfigMap/Secret**: 설정 정보와 민감 데이터 관리
- **PersistentVolume**: 영구 저장소 관리