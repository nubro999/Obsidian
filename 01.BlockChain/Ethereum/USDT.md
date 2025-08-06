
# 1. USDT란?

- **USDT(Tether USD)**는 “1 USDT = 1 USD”로 가치가 고정되도록 설계된 **스테이블코인**입니다.
- **이더리움(ERC-20), 트론(TRC-20), 솔라나 등 다양한 블록체인 네트워크**에 배포되어 있습니다.
- 여기서는 **이더리움(ERC-20)** 기반 USDT를 기준으로 설명하겠습니다.

---

# 2. USDT의 기술적 구조

## 1) **ERC-20 스마트 컨트랙트**

- USDT는 **ERC-20 표준을 준수하는 스마트 컨트랙트**로 구현되어 있습니다.
- 즉, 일반적인 ERC-20 토큰과 동일하게  
  `totalSupply`, `balanceOf`, `transfer`, `approve`, `transferFrom` 등의 함수와  
  `Transfer`, `Approval` 이벤트를 지원합니다.

## 2) **중앙화 발행/소각(Controllable Token)**

- USDT의 **발행(Mint) 및 소각(Burn)** 권한은  
  오직 Tether Limited(회사)의 중앙화된 지갑에만 있습니다.
- 사용자가 Tether사에 달러를 입금하면,  
  Tether사는 **스마트 컨트랙트의 mint 함수를 호출**하여  
  해당 금액만큼의 USDT를 발행해서 사용자에게 전송합니다.
- 반대로 사용자가 USDT를 Tether사에 반환하면,  
  **burn 함수로 USDT를 소각**하고 그에 상응하는 달러를 돌려줍니다.

## 3) **블랙리스트 및 관리 기능**

- USDT 컨트랙트에는  
  **특정 주소의 자산을 동결(freeze)하거나,  
  블랙리스트에 올리는 관리 함수**가 존재합니다.
- 이는 완전한 탈중앙화 토큰과는 다르며,  
  법적 요구나 해킹 등에 대응하기 위한 조치입니다.

---

# 3. USDT ERC-20 스마트 컨트랙트의 주요 함수

| 함수명                       | 설명                                                        |
|-----------------------------|------------------------------------------------------------|
| `transfer`                  | 일반 ERC-20과 동일, 토큰 전송                                |
| `approve`, `transferFrom`   | 위임 송금 관련 ERC-20 표준 함수                              |
| `mint`                      | (관리자만) 새로운 USDT 발행                                 |
| `burn`                      | (관리자만) USDT 소각                                        |
| `addBlackList`, `removeBlackList` | 주소를 블랙리스트에 추가/제거                              |
| `pause`, `unpause`          | 전체 토큰 거래 일시 중지/재개                               |
| `isBlackListed`             | 주소의 블랙리스트 등록 여부 확인                            |
| `redeem`                    | (관리자만) 특정 주소의 자산 몰수(동결 및 소각)              |

---

# 4. 실제 컨트랙트 예시 (단순화)

````solidity
contract TetherToken is ERC20 {
    address public owner;
    mapping(address => bool) public isBlackListed;

    modifier onlyOwner() {
        require(msg.sender == owner, "not owner");
        _;
    }

    function mint(address to, uint amount) public onlyOwner {
        _mint(to, amount);
    }

    function burn(address from, uint amount) public onlyOwner {
        _burn(from, amount);
    }

    function addBlackList(address user) public onlyOwner {
        isBlackListed[user] = true;
    }

    function removeBlackList(address user) public onlyOwner {
        isBlackListed[user] = false;
    }

    function transfer(address to, uint amount) public override returns (bool) {
        require(!isBlackListed[msg.sender], "Blacklisted");
        require(!isBlackListed[to], "Recipient blacklisted");
        return super.transfer(to, amount);
    }
}
````

- 실제 USDT 컨트랙트는 [여기](https://etherscan.io/address/0xdAC17F958D2ee523a2206206994597C13D831ec7#code)에서 확인할 수 있습니다.
- **Proxy 패턴**을 사용하여 업그레이드 가능하게 설계되어 있습니다.

---

# 5. USDT의 특징과 주의사항

- **중앙화**:  
  토큰 발행/소각, 블랙리스트 등 대부분의 권한이  
  Tether사에 집중되어 있음
- **투명성**:  
  모든 USDT 이동 내역은 블록체인에 기록되지만,  
  실제 달러 예치금과 1:1 보증 여부는 Tether사의 외부 감사를 통해 확인해야 함
- **빠른 송금**:  
  USDT는 이더리움 네트워크(ERC-20)에서  
  일반 이더(ETH)와 동일하게 빠르고 저렴하게 송금 가능

---

# 6. 요약

- **USDT(ERC-20)**는  
  ERC-20 표준을 따르는 중앙화 스테이블코인
- Tether사가 발행/소각, 블랙리스트 관리 등  
  주요 권한을 보유
- 다양한 거래소, DApp, 지갑에서  
  **“1 USDT = 1 USD”**로 통용됨
- **완전한 탈중앙화 토큰은 아님**에 유의해야 함

---

추가로,  
- USDT의 스마트 컨트랙트 실제 코드 분석  
- Proxy 패턴, 업그레이드 방식  
- ERC-20 표준과의 미묘한 차이  
- USDT와 USDC, DAI 등 다른 스테이블코인과의 차이  
등이 궁금하다면 언제든 질문해 주세요!