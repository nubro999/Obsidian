

아이디어 
1. 영어페이지도 만들면 좋을듯
2. 폰트깔끔하게
3. nodit은 테스트 및 실습을 좋아함
4. 지원하는 체인 목록/ https://developer.nodit.io/docs/web3-data-api-tutorials 비교
![[[람다256]+1차+인터뷰+사전과제_신형섭님.pdf]]

nodit에서 ai사용하는법
https://developer.nodit.io/docs/nodit-mcp

주요개념들
https://developer.nodit.io/docs/get-started-with-nodit

[[nodit cheat sheet]]
## 노딧의 데이터 추출 핵심 기능

### 1. **ETL 작업 대체**

복잡한 별도의 블록체인 데이터 ETL 작업 없이, 즉시 사용가능하도록 정교하게 인덱싱된 블록체인 데이터에 접근할 수 있는 REST API [Web3 Data API](https://developer.nodit.io/docs/web3-data-api)를 제공합니다.

### 2. **고도화된 인덱싱 엔진**

람다256의 기술력으로 구축한 Web3 인덱스 엔진은 세부적인 수준에서 블록체인 데이터를 인덱싱하고 분석하며, Web3 데이터 레이크 하우스 아키텍처는 대규모의 비정형 데이터를 처리할 수 있는 확장 가능한 데이터 수집과 처리를 보장
### 3. **실시간 데이터 스트리밍**

WebSocket을 통해 블록체인 데이터를 실시간으로 스트리밍하는 도구로, 빠르고 효율적인 데이터 전송과 낮은 지연 시간을 제공 [Stream](https://developer.nodit.io/docs/stream)합니다.

### **개발자가 실제로 원하는 것**

1. **즉시 사용 가능한 데이터**: ETL 구축 없이 바로 조회
2. **의미있는 형태**: 비즈니스 로직에 맞는 구조화된 데이터
3. **실시간 업데이트**: 최신 상태 반영
4. **멀티체인 통합**: 여러 블록체인을 하나의 API로

## 노딧의 데이터 추출 장점

### **1. 검색 유연성**

### **2. 즉시 사용 가능**

### **3. 고성능**

검증된 노드 인프라와 네트워크별 전용 Indexer를 통해 적재된 실시간 온체인 데이터를 제공 [Web3 Data API](https://developer.nodit.io/docs/web3-data-api)합니다.

## 실제 사용 사례로 본 데이터 추출의 중요성

### **거래소 모니터링**

국내 대형 거래소의 불공정거래 모니터링 시스템 [[핀테크경제신문] 람다256의 노딧(Nodit), 베이스(Base) 체인 지원으로 웹3.0 인프라 서비스 확장](https://fintechtimes.co.kr/news/article.html?no=42641)에서 활용되는 것도 결국 복잡한 온체인 데이터를 실시간으로 추출하고 분석하기 위해서입니다.

### **AI 데이터 소비**

AI가 블록체인 상의 데이터 구조를 맥락적으로 이해하고 해석할 수 있도록 문을 열었습니다 [람다256 "노딧 MCP, AI 시대의 블록체인 인터페이스" - ZDNet korea](https://zdnet.co.kr/view/?no=20250520112902). AI가 소비할 수 있는 형태로 데이터를 추출하고 가공하는 것이 핵심입니다.


# Elastic Node
https://developer.nodit.io/docs/elastic-node

# Dedicated Node
https://developer.nodit.io/docs/dedicated-node
Dedicated Node는 전용으로 사용 가능한 고정 자원을 할당한 노드 인프라로, 프로젝트에 더욱 맞춤화되고 일관된 성능을 제공합니다. Dedicated Node는 Elastic Node와 달리 다른 클라이언트와 자원을 공유하지 않으므로 노드의 용량과 성능을 완전히 통제할 수 있습니다. 신뢰할 수 있는 성능이 요구되는 높은 트래픽의 서비스를 제공하는 프로젝트, 노드 인프라에 대한 통제권이 필요한 기업, 또는 엄격한 보안 및 규정 준수가 필요한 프로젝트에 적합한 제품입니다.

# Web3 Data API
https://developer.nodit.io/docs/web3-data-api#%ED%85%9C%ED%94%8C%EB%A6%BF%EC%9D%84-%ED%99%9C%EC%9A%A9%ED%95%9C-api-%ED%98%B8%EC%B6%9C-%EC%98%88%EC%A0%9C-%EC%BD%94%EB%93%9C-%ED%99%9C%EC%9A%A9%ED%95%98%EA%B8%B0
✅ **High Data Reliability**  
검증된 노드 인프라와 네트워크별 전용 Indexer를 통해 적재된 실시간 온체인 데이터를 제공합니다.

✅ **Ready-to-Use Blockchain Data**  
네트워크별로 서로 다른 블록체인 데이터 구조에 대한 깊은 지식과 가공 작업 없이 바로 사용 가능한 직관적인 구조의 블록체인 데이터를 제공합니다.

✅ **Multichain Support**  
다양한 체인 네트워크를 지원합니다. EVM 계열 네트워크를 위한 표준화된 API를 통해 효과적인 데이터 관리가 가능합니다.

✅ **REST API**  
높은 호환성과 사용성을 자랑하는 REST API를 통한 데이터 조회가 가능합니다.

✅ **Key Domains**  
Account(Wallet), Token, NFT, Block, Transaction 등 블록체인 프로젝트에서 가장 많이 사용되는 주요 도메인단위의 API를 제공합니다.


# Stream
https://developer.nodit.io/docs/stream
✅ **Real-time Blockchain Data Stream**  
블록, 트랜잭션, 이벤트, 스마트 컨트랙트의 상태 변화 등 어플리케이션에서 필요한 온체인 이벤트를 실시간 Stream으로 구독할 수 있습니다. 데이터 조회를 매번 요청하는 대신, 연결을 유지함으로서 지속적으로 데이터를 받아볼 수 있어 효과적인 모니터링이 가능합니다.

✅ **Filter Support**  
필요한 데이터만을 효과적으로 선택하여 조회할 수 있도록 다양한 이벤트 필터를 지원합니다.

# Webhook
https://developer.nodit.io/docs/webhook
✅ **Real-time On-chain Notification**  
블록, 트랜잭션, 이벤트, 스마트 컨트랙트의 상태 변화 등 어플리케이션에서 필요한 온체인 이벤트를 실시간으로 구독 할 수 있습니다. 데이터 조회를 매번 요청하거나 Stream 채널을 유지하지 않고 비동기 API 호출을 통한 데이터 조회가 필요하다면 Webhook을 활용한 효과적인 모니터링이 가능합니다.

✅ **Endpoint Registration**  
정의한 이벤트가 발생하는 경우 관련 데이터를 수신할 Endpoint URL을 직접 지정할 수 있으며, 이를 통해 맞춤형 애플리케이션 워크플로우를 설계할 수 있습니다.

✅ **Filter Support**  
트랜잭션, 블록, 이벤트 등 다양한 필터를 활용하여 효과적으로 대상을 모니터링하고, 다양한 조건의 데이터를 각각 다른 Endpoint로 등록하여 수신하는 등의 응용을 통해 복잡한 비즈니스 로직을 쉽게 구현할 수 있습니다.

# Datasquare
https://developer.nodit.io/docs/data-square
Nodit의 강력한 데이터 파이프라인을 무료로 활용해보세요. 방대한 데이터를 저장하기 위한 인프라 비용도, 온체인 데이터들의 수많은 예외사항들에 대한 고려도 필요 없습니다.

✅ **Indexed Blockchain Dataset**  
Nodit의 검증된 체인별 Indexer와 데이터 파이프라인을 통해 적재한 Indexed Dataset, 그 자체가 Datasquare입니다. 데이터를 조회하고, 시각화하고, 기업에서 활용할 수 있는 다양한 데이터 도구와 연동 방식을 지원합니다.

✅ **Query Support**  
관계형 데이터베이스에 적재된 정규화된 블록체인 데이터를 조회하기 위한 쿼리 도구를 지원합니다.

✅ **Data Visualization**  
Datasquare 홈페이지에서 다양한 블록체인 데이터를 활용한 그래프와 대시보드 등의 시각화를 제공합니다.

✅ **Data Pipeline for Enterprise**  
노드 스냅샷, 실시간 블록체인 데이터 구독, 아카이브 데이터 복제 등 기업을 위한 다양한 데이터 연동 옵션을 제공합니다.

graph LR
    A[블록체인 노드] --> B[데이터 수집]
    B --> C[실시간 파싱]
    C --> D[데이터 정제]
    D --> E[인덱싱]
    E --> F[Datasquare 저장]
    F --> G[API 제공]

# sui_devInspectTransactionBlock
https://developer.nodit.io/reference/sui_devinspecttransactionblock

## 1. 트랜잭션 실행 및 시뮬레이션

**개발/테스트 도구**

- `sui_devInspectTransactionBlock`: 트랜잭션 시뮬레이션 (상세 분석)
- `sui_dryRunTransactionBlock`: 트랜잭션 드라이런 (실행 전 검증)

**실제 실행**

- `sui_executeTransactionBlock`: 트랜잭션 실제 실행 및 블록체인 커밋

## 2. 블록체인 상태 조회

**체인 정보**

- `sui_getChainIdentifier`: 체인 식별자 조회
- `sui_getProtocolConfig`: 프로토콜 설정 정보
- `sui_getTotalTransactionBlocks`: 총 트랜잭션 블록 수

**체크포인트 관련**

- `sui_getCheckpoint`: 특정 체크포인트 조회
- `sui_getCheckpoints`: 여러 체크포인트 조회
- `sui_getLatestCheckpointSequenceNumber`: 최신 체크포인트 번호

## 3. 객체 및 데이터 조회

**객체 조회**

- `sui_getObject`: 단일 객체 조회
- `sui_multiGetObjects`: 여러 객체 일괄 조회
- `sui_tryGetPastObject`: 과거 객체 상태 조회
- `sui_tryMultiGetPastObjects`: 여러 과거 객체 상태 조회

**트랜잭션 조회**

- `sui_getTransactionBlock`: 특정 트랜잭션 블록 조회
- `sui_multiGetTransactionBlocks`: 여러 트랜잭션 블록 조회

**이벤트**

- `sui_getEvents`: 이벤트 조회

## 4. Move 언어 관련 (스마트 컨트랙트)

**함수 정보**

- `sui_getMoveFunctionArgTypes`: Move 함수 인수 타입
- `sui_getNormalizedMoveFunction`: 정규화된 Move 함수

**모듈 정보**

- `sui_getNormalizedMoveModule`: 정규화된 Move 모듈
- `sui_getNormalizedMoveModulesByPackage`: 패키지별 Move 모듈들
- `sui_getNormalizedMoveStruct`: 정규화된 Move 구조체

## 5. SUIX - 확장 기능들

**잔액 및 코인 관리**

- `suix_getAllBalances`: 모든 토큰 잔액
- `suix_getAllCoins`: 모든 코인 조회
- `suix_getBalance`: 특정 토큰 잔액
- `suix_getCoinMetadata`: 코인 메타데이터
- `suix_getCoins`: 코인 조회
- `suix_getTotalSupply`: 총 공급량

**소유권 및 객체**

- `suix_getOwnedObjects`: 소유 객체 조회
- `suix_getDynamicFieldObject`: 동적 필드 객체
- `suix_getDynamicFields`: 동적 필드들

**스테이킹 관련**

- `suix_getStakes`: 스테이킹 정보
- `suix_getStakesByIds`: ID별 스테이킹 정보
- `suix_getValidatorsApy`: 검증자 APY
- `suix_getCommitteeInfo`: 위원회 정보
- `suix_getLatestSuiSystemState`: 최신 Sui 시스템 상태

**가격 및 시스템**

- `suix_getReferenceGasPrice`: 기준 가스 가격

**검색 및 쿼리**

- `suix_queryEvents`: 이벤트 쿼리
- `suix_queryTransactionBlocks`: 트랜잭션 블록 쿼리

**네임 서비스**

- `suix_resolveNameServiceAddress`: 이름 → 주소 해석
- `suix_resolveNameServiceNames`: 주소 → 이름 해석

**구독 (실시간)**

- `suix_subscribeEvent`: 이벤트 구독
- `suix_subscribeTransaction`: 트랜잭션 구독

## 6. UNSAFE - 트랜잭션 생성 도구들

**코인 관리**

- `unsafe_mergeCoins`: 코인 병합
- `unsafe_splitCoin`: 코인 분할
- `unsafe_splitCoinEqual`: 코인 균등 분할

**전송**

- `unsafe_transferObject`: 객체 전송
- `unsafe_transferSui`: SUI 토큰 전송
- `unsafe_pay`: 결제
- `unsafe_payAllSui`: 모든 SUI 결제
- `unsafe_paySui`: SUI 결제

**스마트 컨트랙트**

- `unsafe_moveCall`: Move 함수 호출
- `unsafe_publish`: 컨트랙트 배포

**스테이킹**

- `unsafe_requestAddStake`: 스테이킹 추가 요청
- `unsafe_requestWithdrawStake`: 스테이킹 출금 요청

**일괄 처리**

- `unsafe_batchTransaction`: 배치 트랜잭션

**인증**

- `sui_verifyZkLoginSignature`: zkLogin 서명 검증

## 사용 패턴

**DApp 개발 시**: `suix_*` 메서드들로 데이터 조회, `unsafe_*`로 트랜잭션 구성, `sui_devInspectTransactionBlock`으로 테스트 후 `sui_executeTransactionBlock`으로 실행하는 플로우가 일반적입니다.

## sui - 코어 블록체인 기능

**기준**: Sui 블록체인의 핵심 프로토콜 기능들

- 블록체인 상태 조회 (체크포인트, 트랜잭션, 객체)
- 트랜잭션 실행 및 시뮬레이션
- Move 언어 관련 메타데이터
- 프로토콜 수준의 기본 기능들

**특징**:

- 블록체인 노드가 기본적으로 제공해야 하는 표준 기능
- 다른 Sui 클라이언트 구현체들도 동일하게 제공해야 하는 API
- 프로토콜 사양에 정의된 기능들

## suix - 확장 편의 기능

**기준**: 개발자 편의를 위한 확장된 기능들 (Extended functions)

- 복잡한 쿼리를 단순화한 래퍼 함수들
- 여러 기본 API를 조합한 고수준 기능
- DApp 개발에 특화된 유틸리티 함수들

**특징**:

- `sui_*` 메서드들을 조합하여 만들 수 있지만, 편의성을 위해 제공
- 실시간 구독, 복합 쿼리, 잔액 조회 등 실용적 기능
- 클라이언트 구현체마다 다를 수 있는 확장 기능

**예시**:

- `suix_getAllBalances`는 여러 `sui_getObject` 호출을 조합한 것
- `suix_getOwnedObjects`는 소유권 필터링을 추가한 편의 기능

## unsafe - 트랜잭션 구성 도구

**기준**: 서명되지 않은 트랜잭션을 생성하는 도구들

- 클라이언트에서 트랜잭션을 구성할 때 사용
- 실제 실행 전 트랜잭션 바이트코드를 생성

**"unsafe"인 이유**:

- **서명되지 않은 상태**: 아직 개인키로 서명하지 않은 트랜잭션
- **검증되지 않은 상태**: 실행 전까지는 유효성이 보장되지 않음
- **잘못 사용 시 위험**: 부적절한 매개변수로 자산 손실 가능성

**워크플로우**:

1. `unsafe_*`로 트랜잭션 구성
2. 클라이언트에서 개인키로 서명
3. `sui_executeTransactionBlock`로 실행

## 설계 철학

이런 분류는 **책임의 분리**를 나타냅니다:

- **sui**: 블록체인 코어가 보장해야 할 기본 기능
- **suix**: 생태계 발전을 위한 개발자 친화적 확장
- **unsafe**: 클라이언트 측 트랜잭션 구성 도구 (보안 주의 필요)

다른 블록체인들도 비슷한 패턴을 가지고 있어요. 예를 들어 Ethereum의 경우 `eth_*` (코어), `net_*` (네트워크), `personal_*` (위험한 개인키 관련) 등으로 분류하죠.

# 🚀 Nodit Sui API Hackathon CheatSheet

## 🏗️ 기본 설정

javascript

```javascript
const NODIT_ENDPOINT = "https://api.nodit.io/v1/sui";
const API_KEY = "your_api_key_here";

const callNoditAPI = async (method, params) => {
  const response = await fetch(NODIT_ENDPOINT, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'X-API-KEY': API_KEY
    },
    body: JSON.stringify({
      jsonrpc: "2.0",
      id: 1,
      method,
      params
    })
  });
  return response.json();
};
```

## 🎯 핵심 워크플로우

### 1️⃣ 사용자 지갑 정보 조회

**필수 API**: `suix_getOwnedObjects`, `suix_getAllBalances`

javascript

```javascript
// 1. 사용자 소유 객체 조회
const getWalletInfo = async (address) => {
  // 모든 잔액 조회
  const balances = await callNoditAPI("suix_getAllBalances", [address]);
  
  // 소유 객체 조회 (NFT, 기타 객체)
  const objects = await callNoditAPI("suix_getOwnedObjects", [
    address,
    {
      filter: null,
      options: {
        showType: true,
        showContent: true,
        showDisplay: true
      }
    }
  ]);
  
  return { balances: balances.result, objects: objects.result };
};
```

### 2️⃣ 트랜잭션 구성 → 테스트 → 실행

**필수 API**: `unsafe_*` → `sui_devInspectTransactionBlock` → `sui_executeTransactionBlock`

javascript

```javascript
// Step 1: 트랜잭션 구성 (예: SUI 전송)
const createTransferTx = async (sender, recipient, amount) => {
  return await callNoditAPI("unsafe_transferSui", [
    sender,
    recipient,
    amount
  ]);
};

// Step 2: 실행 전 테스트
const testTransaction = async (txBytes, sender) => {
  return await callNoditAPI("sui_devInspectTransactionBlock", [
    txBytes,
    sender
  ]);
};

// Step 3: 실제 실행
const executeTransaction = async (txBytes) => {
  return await callNoditAPI("sui_executeTransactionBlock", [
    txBytes,
    { request_type: "WaitForLocalExecution" }
  ]);
};

// 완전한 워크플로우
const safeSuiTransfer = async (sender, recipient, amount) => {
  // 1. 트랜잭션 구성
  const txResult = await createTransferTx(sender, recipient, amount);
  const txBytes = txResult.result;
  
  // 2. 실행 전 테스트
  const testResult = await testTransaction(txBytes, sender);
  if (testResult.result.effects.status !== "success") {
    throw new Error("Transaction would fail:", testResult.result);
  }
  
  console.log("예상 가스 비용:", testResult.result.effects.gasUsed);
  
  // 3. 실제 실행
  const execResult = await executeTransaction(txBytes);
  return execResult;
};
```

### 3️⃣ 스마트 컨트랙트 상호작용

**필수 API**: `unsafe_moveCall`, `sui_getNormalizedMoveFunction`

javascript

```javascript
// 컨트랙트 함수 정보 조회
const getContractInfo = async (packageId, moduleName, functionName) => {
  return await callNoditAPI("sui_getNormalizedMoveFunction", [
    packageId,
    moduleName,
    functionName
  ]);
};

// Move 함수 호출
const callMoveFunction = async (packageId, module, func, args, typeArgs) => {
  const txBytes = await callNoditAPI("unsafe_moveCall", [
    packageId,
    module,
    func,
    typeArgs || [],
    args || []
  ]);
  
  // 테스트 후 실행
  const testResult = await testTransaction(txBytes.result, sender);
  if (testResult.result.effects.status === "success") {
    return await executeTransaction(txBytes.result);
  }
  throw new Error("Move call would fail");
};
```

### 4️⃣ 실시간 이벤트 모니터링

**필수 API**: `suix_subscribeEvent`, `suix_queryEvents`

javascript

```javascript
// 이벤트 구독 (WebSocket 필요)
const subscribeToEvents = async (eventFilter) => {
  return await callNoditAPI("suix_subscribeEvent", [eventFilter]);
};

// 과거 이벤트 쿼리
const queryPastEvents = async (query, cursor = null, limit = 50) => {
  return await callNoditAPI("suix_queryEvents", [
    query,
    cursor,
    limit,
    true // descending order
  ]);
};

// 특정 컨트랙트 이벤트 조회
const getContractEvents = async (packageId) => {
  return await queryPastEvents({
    MoveModule: {
      package: packageId,
      module: "your_module_name"
    }
  });
};
```

## 🔧 필수 유틸리티 함수

### 가스 가격 조회

javascript

```javascript
const getGasPrice = async () => {
  const result = await callNoditAPI("suix_getReferenceGasPrice", []);
  return result.result;
};
```

### 객체 상세 정보 조회

javascript

```javascript
const getObjectDetails = async (objectId) => {
  return await callNoditAPI("sui_getObject", [
    objectId,
    {
      showType: true,
      showContent: true,
      showDisplay: true,
      showPreviousTransaction: true
    }
  ]);
};
```

### 트랜잭션 결과 조회

javascript

```javascript
const getTransactionDetails = async (txHash) => {
  return await callNoditAPI("sui_getTransactionBlock", [
    txHash,
    {
      showInput: true,
      showEffects: true,
      showEvents: true,
      showObjectChanges: true
    }
  ]);
};
```

## 📊 DApp별 주요 패턴

### NFT 마켓플레이스

javascript

```javascript
// 1. 사용자 NFT 조회
const getUserNFTs = async (address) => {
  return await callNoditAPI("suix_getOwnedObjects", [
    address,
    { filter: { StructType: "0x2::nft::NFT" } }
  ]);
};

// 2. NFT 전송
const transferNFT = async (sender, recipient, nftObjectId) => {
  const txBytes = await callNoditAPI("unsafe_transferObject", [
    sender,
    nftObjectId,
    recipient
  ]);
  return await executeWithTest(txBytes.result, sender);
};
```

### DeFi 애플리케이션

javascript

```javascript
// 1. 코인 잔액 및 메타데이터
const getCoinInfo = async (coinType) => {
  const metadata = await callNoditAPI("suix_getCoinMetadata", [coinType]);
  const supply = await callNoditAPI("suix_getTotalSupply", [coinType]);
  return { metadata: metadata.result, supply: supply.result };
};

// 2. 코인 분할/병합
const splitCoins = async (sender, coinObjectId, amounts) => {
  const txBytes = await callNoditAPI("unsafe_splitCoin", [
    sender,
    coinObjectId,
    amounts
  ]);
  return await executeWithTest(txBytes.result, sender);
};
```

### 게임 DApp

javascript

```javascript
// 1. 동적 필드 조회 (게임 상태)
const getGameState = async (gameObjectId) => {
  const fields = await callNoditAPI("suix_getDynamicFields", [gameObjectId]);
  return fields.result;
};

// 2. 게임 액션 실행
const performGameAction = async (packageId, actionFunction, gameArgs) => {
  return await callMoveFunction(
    packageId,
    "game",
    actionFunction,
    gameArgs,
    []
  );
};
```

## ⚡ 성능 최적화 팁

1. **배치 요청 사용**: 여러 객체 조회 시 `sui_multiGetObjects` 활용
2. **필터링 활용**: `suix_getOwnedObjects`에서 정확한 필터 사용
3. **캐싱**: 변하지 않는 메타데이터는 로컬 캐싱
4. **이벤트 구독**: 실시간 업데이트가 필요한 경우만 사용

## 🚨 주의사항

- **항상 `devInspectTransactionBlock`으로 테스트 후 실행**
- **가스 한도 설정 주의**
- **타입 인수 정확히 명시**
- **에러 처리 필수**

## 🔗 빠른 참조

|기능|주요 API|용도|
|---|---|---|
|지갑 조회|`suix_getOwnedObjects`, `suix_getAllBalances`|사용자 자산 표시|
|전송|`unsafe_transferSui`, `unsafe_transferObject`|자산 이동|
|컨트랙트 호출|`unsafe_moveCall`|스마트 컨트랙트 상호작용|
|테스트|`sui_devInspectTransactionBlock`|실행 전 검증|
|실행|`sui_executeTransactionBlock`|트랜잭션 실행|
|모니터링|`suix_queryEvents`, `suix_subscribeEvent`|이벤트 추적|

---

**💡 해커톤 성공 팁**: 먼저 기본 전송부터 구현하고, 점진적으로 복잡한 기능을 추가하세요!

