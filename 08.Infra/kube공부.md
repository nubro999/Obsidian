[[kube기본개념]]
[[Kubernetes]]
[[kubenetes학습]]
[[docs스크랩]]

## 1주차: 기초 다지기 + 아키텍처 이해

**1-3일차: 쿠버네티스 기본 개념**

- 공식 docs의 Concepts 섹션 정독 (Pod, Service, Deployment 등)
- minikube나 kind로 로컬 클러스터 구축
- kubectl 명령어로 직접 리소스 생성/조회/삭제 연습
- 목표: 쿠버네티스가 "무엇을 해결하는지" 체감

**4-7일차: 아키텍처 깊이 파기**

- Control Plane 컴포넌트 이해 (API Server, Scheduler, Controller Manager, etcd)
- Node 컴포넌트 이해 (kubelet, kube-proxy, container runtime)
- 공식 문서의 "Kubernetes Components" 반복 학습
- `kubectl get pods -n kube-system`으로 실제 컴포넌트 확인
- 각 컴포넌트의 역할과 통신 흐름 다이어그램 직접 그려보기

## 2주차: 소스코드 진입 + 개발환경 구축

**8-10일차: 개발환경 셋업**

- kubernetes/kubernetes 레포 클론
- 로컬 빌드 환경 구축 (Go 1.21+)
- `make` 명령으로 빌드 테스트
- 변경하려는 모듈 위치 파악 (cmd/, pkg/, staging/ 구조 이해)

**11-14일차: 코드 읽기 시작**

- 변경할 컴포넌트의 main.go부터 추적
- 해당 컴포넌트의 초기화 과정 따라가기
- 핵심 인터페이스와 구조체 파악
- 주석과 godoc 활용
- 작은 함수부터 읽고 점진적으로 확장

**팁**: 처음엔 모든 코드를 이해하려 하지 말고, 변경할 부분과 직접 연관된 코드 경로만 집중

## 3주차: 실습 + 디버깅

**15-17일차: 로컬에서 수정 및 테스트**

- 간단한 로그 추가나 작은 기능 수정 시도
- 로컬 클러스터에 수정한 바이너리 배포
- `kubectl logs`, `kubectl describe` 로 동작 확인
- Delve 같은 Go 디버거 사용해보기

**18-21일차: 런타임 분석**

- `--v=5` 같은 verbosity 플래그로 상세 로그 보기
- API 요청 흐름 추적 (kube-apiserver 로그)
- 이벤트 스트림 모니터링 (`kubectl get events --watch`)
- Prometheus metrics 활용 (컴포넌트별 `/metrics` 엔드포인트)

## 4주차: 심화 + 실전 시뮬레이션

**22-24일차: 테스트 작성**

- 기존 unit test 분석 (`*_test.go` 파일들)
- 수정한 코드에 대한 테스트 작성
- integration test 실행해보기
- E2E 테스트 개념 이해

**25-28일차: 실전 준비**

- 실제 변경하려는 기능 명확히 정의
- 해당 변경이 영향 미치는 범위 분석
- 코드 변경 시뮬레이션 (실제 커밋 전 연습)
- 관련 KEP(Kubernetes Enhancement Proposal) 읽기
- 커뮤니티 Slack/GitHub Issues에서 유사 케이스 검색

## 병행할 활동들

**매일 30분씩**:

- Kubernetes 블로그나 YouTube 영상 (공식 채널 추천)
- SIG(Special Interest Group) 미팅 녹화본 시청

**주 1회**:

- 전체 학습 내용 정리 및 회고
- 막혔던 부분 재점검
- 메가존이랑 컨택해라
- 플랫폼을 볼 수 있나? >> 2월에 나옴