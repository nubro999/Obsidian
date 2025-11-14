
- [ ] 런팟이 어떻게 작동하는 지 알아보기 (gpu대여, 쿠버네티스, 토크노믹스)
- [ ] 



[[runpod IR]]

WebRTC사용해서 p2p방식으로 파일전송

SSH(Secure Shell) 기반 파일전송

Pod이 실행되면 자동으로 **SSH 접속**과 **Web Proxy URL**을 제공

ex) runpodctl send <Pod ID> <로컬 파일 경로> <원격 경로>

기존의 runpod 코드를 고쳐서 Kube의 Service및 Ingress와 같은 복잡한 네트워킹 추상화 계층을 생략

과금 전략 : 시작 및 중지이벤트감지, 자체 모니터링 에이전트, 실시간 정산

백엔드의 역할: off 체인에서 사용량을 측정하고 백엔드는 이 결과를 컨트랙트 함수(예: Payment(userAddress, providerAddress, durationInSeconds, gpuType))를 호출하는 트랜잭션으로 변환하여 블록체인에 제출

핫 월렛 방식으로 지갑관리

https://github.com/runpod/runpodctl
https://github.com/runpod-workers/worker-comfyui

코드 분석 후 온체인 연결
