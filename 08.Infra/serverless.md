
[Event Source] → [API Gateway/Event Trigger] → [Lambda/Cloud Function] → [Response]
```

### 2. **주요 구성 요소**

**API Gateway**
- RESTful API 엔드포인트 제공
- 요청 라우팅 및 인증/권한 관리
- 트래픽 관리 및 throttling

**함수 실행 환경**
- AWS Lambda, Google Cloud Functions, Azure Functions 등
- 콜드 스타트: 새 컨테이너 초기화 (수백ms~수초)
- 웜 스타트: 기존 컨테이너 재사용 (수ms)

**이벤트 소스**
- HTTP 요청 (API Gateway)
- 메시지 큐 (SQS, Pub/Sub)
- 스트림 (Kinesis, Kafka)
- 스케줄러 (Cron)
- 데이터베이스 트리거

### 3. **실행 플로우**
```
1. 이벤트 발생
   ↓
2. 이벤트 라우팅 (API Gateway/EventBridge)
   ↓
3. 함수 인스턴스 준비
   - 기존 컨테이너 있음? → 재사용 (웜 스타트)
   - 없음? → 새 컨테이너 생성 (콜드 스타트)
   ↓
4. 함수 실행
   ↓
5. 응답 반환
   ↓
6. 컨테이너 유지 (일정 시간) 또는 종료
```

## 전통적 아키텍처와의 비교

**전통적 서버 기반**
```
[Load Balancer] → [Server 1] → [App Container]
                  [Server 2] → [App Container]
                  [Server 3] → [App Container]
```
- 항상 실행 중
- 고정 용량
- 서버 관리 필요

**Serverless**
```
[API Gateway] → [Lambda 1] (요청 시에만 실행)
                [Lambda 2] (자동 확장)
                [Lambda N] (무제한 병렬 처리)
```
- 요청당 실행
- 자동 확장
- 관리 불필요

## 아키텍처 패턴

### 1. **마이크로서비스 패턴**
```
User → API Gateway → Lambda (User Service)
                   → Lambda (Order Service)
                   → Lambda (Payment Service)
```

### 2. **이벤트 기반 패턴**
```
S3 Upload → Lambda (Image Processing)
          → Lambda (Thumbnail Generation)
          → Lambda (DB Update)
```

### 3. **CQRS 패턴**
```
Write: API → Lambda → DynamoDB
Read: API → Lambda → ElastiCache/Read Replica
```

## DApp과의 연관성

블록체인 DApp 개발 시 serverless는 다음과 같이 활용됩니다:

**백엔드 서비스**
```
DApp Frontend → API Gateway → Lambda
                             ↓
                          Web3.js/Ethers.js
                             ↓
                          Blockchain Node