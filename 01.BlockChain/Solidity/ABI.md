
# 1. **ABI란 무엇인가?**

- **ABI**는 **Application Binary Interface**의 약자입니다.
- 이더리움에서 **스마트컨트랙트와 외부(예: DApp, 다른 컨트랙트, 프론트엔드)가 상호작용할 때 사용하는 표준화된 인터페이스**입니다.
- ABI는 컨트랙트의 **함수, 입력/출력 타입, 이벤트** 등의 정보를 담고 있어,  
    **컨트랙트와 외부 프로그램이 서로를 이해하고 호출할 수 있게 해줍니다.**

---

## 2. **ABI의 필요성**

- 스마트컨트랙트는 바이트코드 형태로 블록체인에 배포됩니다.  
    이 바이트코드는 사람이 읽을 수 없고, 함수 이름이나 타입 정보가 없습니다.
- 외부에서 컨트랙트의 함수를 호출하려면,  
    함수의 **이름**, **파라미터 타입**, **반환 타입** 등 정보를 알아야 합니다.
- ABI가 바로 이 정보를 표준 규격(JSON)으로 제공합니다.

---

# 3. [[ABI의 형식]]

- **JSON 배열** 형태로, 각 요소는 함수, 이벤트, 에러 등에 대한 정보를 담은 객체입니다.
- 대표적인 필드:
    - `type`: `"function"`, `"constructor"`, `"event"`, `"fallback"`, `"receive"`, `"error"`
    - `name`: 함수/이벤트/에러의 이름
    - `inputs`: 입력 파라미터 배열(각각 `{ name, type, ... }`)
    - `outputs`: 출력 파라미터 배열(함수만)
    - `stateMutability`: `"pure"`, `"view"`, `"nonpayable"`, `"payable"`
    - `anonymous`: 이벤트 전용(익명 이벤트인지)
    - 기타: `indexed`(이벤트 파라미터), `constant`(구버전), 등


---

### **예시**


`[   {     "type": "function",     "name": "balanceOf",     "inputs": [{"name": "owner", "type": "address"}],     "outputs": [{"name": "balance", "type": "uint256"}],     "stateMutability": "view"   },   {     "type": "event",     "name": "Transfer",     "inputs": [       {"name": "from", "type": "address", "indexed": true},       {"name": "to", "type": "address", "indexed": true},       {"name": "value", "type": "uint256", "indexed": false}     ],     "anonymous": false   } ]`

---

## 4. **각 필드 설명**

| 필드명             | 설명                                               |
| --------------- | ------------------------------------------------ |
| type            | 요소의 종류: function, event, constructor, fallback 등 |
| name            | 함수/이벤트/에러 이름                                     |
| inputs          | 입력 파라미터 배열(각각 name, type, indexed 등)             |
| outputs         | 출력 파라미터 배열(함수만 해당)                               |
| stateMutability | 상태 변경/이더 송금 여부: pure, view, nonpayable, payable  |
| anonymous       | 이벤트에서만 사용, 익명 이벤트 여부                             |

---

# 5. **ABI와 실제 상호작용**

- 프론트엔드(Web3.js, Ethers.js 등)는 ABI를 이용해  
    컨트랙트의 함수/이벤트를 **자동으로 인식**하고,  
    올바른 방식으로 **함수 호출 트랜잭션을 생성**합니다.
- ABI는 컨트랙트 배포 시 자동 생성되며,  
    배포 후에는 컨트랙트 주소와 ABI만 있으면 어디서든 상호작용이 가능합니다.

---

## **정리**

- ABI는 스마트컨트랙트와 외부 세계(프론트, 다른 컨트랙트 등)의 **약속된 통신 규약**
- 함수, 이벤트, 입력/출력 타입 등 **인터페이스 정보**를 JSON 배열로 표현
- 프론트엔드와의 연동, 자동 호출, 타입 체크 등에 필수적

