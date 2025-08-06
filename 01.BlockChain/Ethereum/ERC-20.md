
```solidity

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleToken {
    string public name = "SimpleToken";
    string public symbol = "STK";
    uint8 public decimals = 18;
    uint public totalSupply = 1000000 * (10 ** uint(decimals));
    mapping(address => uint) public balanceOf;
    mapping(address => mapping(address => uint)) public allowance;

    event Transfer(address indexed from, address indexed to, uint value);
    event Approval(address indexed owner, address indexed spender, uint value);

    constructor() {
        balanceOf[msg.sender] = totalSupply;
    }

    function transfer(address to, uint value) public returns (bool) {
        require(balanceOf[msg.sender] >= value, "Not enough balance");
        balanceOf[msg.sender] -= value;
        balanceOf[to] += value;
        emit Transfer(msg.sender, to, value);
        return true;
    }

    function approve(address spender, uint value) public returns (bool) {
        allowance[msg.sender][spender] = value;
        emit Approval(msg.sender, spender, value);
        return true;
    }

    function transferFrom(address from, address to, uint value) public returns (bool) {
        require(balanceOf[from] >= value, "Not enough balance");
        require(allowance[from][msg.sender] >= value, "Not enough allowance");
        balanceOf[from] -= value;
        balanceOf[to] += value;
        allowance[from][msg.sender] -= value;
        emit Transfer(from, to, value);
        return true;
    }
}

```


# 1. ERC-20이란?

- **ERC-20**은 “Ethereum Request for Comments 20”의 약자입니다.
- **이더리움 블록체인에서 토큰을 만들고, 관리하고, 교환하는 표준 인터페이스**입니다.
- 누구나 이 표준에 따라 스마트 컨트랙트를 작성하면  
    **호환되는 지갑, 거래소, DApp 등에서 자유롭게 토큰을 주고받을 수 있습니다.**

---

# 2. 왜 중요한가?

- 다양한 프로젝트(DeFi, 게임, DAO 등)에서  
    자체 토큰(예:[[ USDT]], UNI, AAVE 등)을 만들 때 **ERC-20 표준**을 사용합니다.
- **상호 운용성**:  
    모든 ERC-20 토큰은 같은 방식으로 동작하므로,  
    지갑, 거래소, DApp 등에서 쉽게 지원할 수 있습니다.
    
# 3. 주요 기능/함수

ERC-20 표준은 다음과 같은 **함수와 이벤트**를 반드시 구현해야 합니다.

|함수명|설명|
|---|---|
|`totalSupply()`|토큰의 총 발행량 반환|
|`balanceOf(address)`|특정 주소의 토큰 잔액 반환|
|`transfer(to, amount)`|내 지갑에서 다른 주소로 토큰 전송|
|`approve(spender, amount)`|다른 주소(스마트 컨트랙트 등)가 내 토큰을 일정량 사용할 수 있도록 승인|
|`allowance(owner, spender)`|승인된 토큰 한도 확인|
|`transferFrom(from, to, amount)`|승인받은 토큰을 제3자가 대신 전송|

**이벤트**

- `Transfer`: 토큰이 전송될 때 발생
- `Approval`: 토큰 사용 권한 승인 시 발생