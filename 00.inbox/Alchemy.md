
# 1. Alchemy란?

- **Alchemy**는 이더리움(Ethereum), Polygon, Optimism, Arbitrum, Solana 등 다양한 블록체인 네트워크에 대한 **노드 인프라 서비스**와 개발 툴을 제공합니다.
- 쉽게 말해, **블록체인 애플리케이션(디앱, NFT, DeFi 등)을 만들 때 필요한 백엔드 인프라를 손쉽게 쓸 수 있게 해주는 서비스**입니다.

---

# 2. 왜 필요한가?

- 블록체인 앱을 만들려면 직접 **노드(Node)**를 운영해야 하지만,  
  노드 설치/운영/유지보수는 매우 복잡하고 비용이 많이 듭니다.
- Alchemy는 이런 복잡한 과정을 대신 처리해 주고,  
  **빠르고 안정적인 API**를 통해 블록체인과 상호작용할 수 있게 해줍니다.

---

# 3. 주요 기능 및 서비스

## 1) **블록체인 노드 API**

- **JSON-RPC API**: 이더리움 등 블록체인과 통신할 때 표준적으로 쓰는 API를 제공합니다.
- **WebSocket 지원**: 실시간 이벤트(예: 트랜잭션, 블록 생성 등) 감지 가능.

## 2) **Enhanced API**

- Alchemy만의 고급 기능(예: 빠른 트랜잭션 추적, NFT API, 토큰 밸런스 조회 등)을 제공합니다.
- 예시:
  - **alchemy_getAssetTransfers**: 계정의 자산 이동 내역을 쉽게 조회
  - **alchemy_getTokenBalances**: 주소의 토큰 잔고를 한 번에 조회

## 3) **NFT API**

- NFT 메타데이터, 소유자, 거래 내역 등을 쉽게 가져올 수 있는 API 제공

## 4) **Monitoring & Analytics**

- 대시보드에서 트래픽, 에러, 사용량 등 실시간 모니터링 가능

## 5) **Webhooks & Notifier**

- 특정 이벤트(예: 트랜잭션 발생, 잔고 변화 등)가 발생하면 알림(Webhook) 받기

## 6) **Developer Tools**

- **Composer**: API 요청을 웹에서 테스트해볼 수 있는 툴
- **Explorer**: 스마트 컨트랙트, 트랜잭션, 블록 탐색기
- **Mempool Visualizer**: 미확정 트랜잭션 실시간 확인

---

# 4. 지원하는 네트워크

- **Ethereum Mainnet/Testnet(Goerli, Sepolia 등)**
- **Polygon**
- **Optimism**
- **Arbitrum**
- **Solana**
- **Starknet**
- 등 다양한 L2, Sidechain, Layer1 등 지원

---

# 5. 사용 예시

## 1) **이더리움 노드 연결**

```javascript
const { Alchemy, Network } = require("alchemy-sdk");

const settings = {
  apiKey: "YOUR_ALCHEMY_API_KEY",
  network: Network.ETH_MAINNET,
};

const alchemy = new Alchemy(settings);

alchemy.core.getBlockNumber().then(console.log);
```

## 2) **NFT 정보 가져오기**

```javascript
alchemy.nft.getNftsForOwner("0x1234...").then(console.log);
```

## 3) **트랜잭션 전송**

- 웹3.js, ethers.js와 연동해서 Alchemy의 엔드포인트를 사용 가능

---

# 6. Alchemy vs Infura

- **Infura**도 비슷한 블록체인 노드 서비스지만,  
  Alchemy는 더 다양한 개발자 도구, 고급 API, 모니터링, NFT 지원 등에서 강점을 가집니다.
- 대시보드, 분석, Webhook 등 부가 기능이 더 풍부합니다.

---

# 7. 요금제

- **무료 플랜**도 제공하며,  
  요청 수(API Call)에 따라 유료 플랜으로 업그레이드 할 수 있습니다.

---

# 8. 실제 사용처

- OpenSea, 0x, Dapper Labs 등  
  대형 NFT/DeFi 서비스들도 Alchemy 인프라를 사용합니다.

---

# 9. 공식 사이트 및 문서

- [Alchemy 공식 홈페이지](https://alchemy.com/)
- [Alchemy 공식 문서](https://docs.alchemy.com/)
