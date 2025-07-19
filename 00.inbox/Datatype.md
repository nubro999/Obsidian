
# Primitive Data Types

Solidity의 기본 데이터 타입에는 `boolean` `uint` `int` `address` `byte` 등이 있다. 
### 선언 방법
![[Pasted image 20250719213051.png]]
<타입> <접근지정자> <변수명> = <값>;

## Boolean 
`bool` 타입은 참(True) 또는 거짓(False) 값을 가질 수 있는 데이터 타입이다. 
```solidity
bool public boo = true;
```
> public 가시성에 대해서는 나중에 다시 배운다. 쉽게 말해 접근 지정자.

## Unsigned Integer
`uint` 는 부호가 없는 정수,  즉 양수만을 표현한다.

- **크기 및 범위** :  
    - `uint8` : 0 ~ 2^8 - 1 (0 ~ 255)
    - `uint16` : 0 ~ 2^16 - 1 (0 ~ 65535)
    - ...
    - `uint256` : 0 ~ 2^256 - 1 
    
    뒤에 붙는 숫자는 bit 수를 의미한다. 8비트(1 byte) 단위로 선언할 수 있다. 
```solidity
uint8 public u8 = 1;
uint256 public u256 = 456;
uint public u = 123; // uint는 uint256의 별칭이다.
```

## Signed Integer
`int` 부호 있는 정수
- **크기 및 범위** :  
    - `int8` : -2^7 ~ 2^7 - 1 (-128 ~ 127)
    - `int16` : -2^15 ~ 2^15 - 1
    - ...
    - `int256` : -2^255 ~ 2^255 - 1 

    마찬가지로 8비트 단위로 선언 가능하다. 
```solidity
int8 public i8 = -1;
int256 public i256 = 456;
int public i = -123; // int는 int256과 동일하다.
```

* 최소값과 최대값 :
``` solidity
int256 public minInt = type(int256).min; // -2^255
int public maxInt = type(int256).max; // 2^255 - 1
```

## Address
`address` 타입은 이더리움 주소를 저장하는 데 사용된다.주소는 **20바이트(160비트)** 크기이다.
```solidity
address public addr = 0xCA35b7d915458EF540aDe6068dFe2F44E8fa733c;
```

## Bytes
`byte` 타입은 바이트의 시퀀스를 나타낸다. 두가지 타입의 배열이 있다. 

1. 고정 크기 바이트 배열 : `bytes1`, `bytes2`, ..., `bytes32`  
최대 32바이트까지 가능. 고정 크기라서 배열의 길이를 따로 저장하지 않는다. 
2. 동적 크기 바이트 배열 : `bytes`
byte[]의 축약형이다. 배열 길이를 포함하여 저장한다. 
```solidity
bytes1 public a = 0Xb5; //1바이트 크기, 값은 [10110101]
bytes public dynamicBytes="Hello"; //ASCII 값으로 저장
```

---
---
### **기본값** 
변수가 초기화 되지 않을 시엔 기본값이 자동으로 설정된다. 
```solidity
bool public defaultBoo; // false
uint256 public defaultUint; // 0
int256 public defaultInt; // 0
address public defaultAddr; // 0x0000000000000000000000000000000000000000
bytes2 public defaultBytes2;  // 기본값: 0x0000
bytes public defaultBytes;  // 기본값: 빈 배열 (길이 0)
```

---

### 예제코드 
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract Primitives {
    bool public boo = true;

    /*
    uint는 부호 없는 정수를 의미하며, 음수가 아닌 정수이다.
    다양한 크기의 부호 없는 정수가 제공됩니다.
        uint8   범위: 0 ~ 2 ** 8 - 1
        uint16  범위: 0 ~ 2 ** 16 - 1
        ...
        uint256 범위: 0 ~ 2 ** 256 - 1
    */
    uint8 public u8 = 1;
    uint256 public u256 = 456;
    uint256 public u = 123; // uint는 uint256의 별칭이다.

    /*
    int 타입은 음수를 허용한다.
    uint와 마찬가지로 다양한 크기의 부호 있는 정수가 제공된다.
    
    int256의 범위: -2 ** 255 ~ 2 ** 255 - 1
    int128의 범위: -2 ** 127 ~ 2 ** 127 - 1
    */
    int8 public i8 = -1;
    int256 public i256 = 456;
    int public i = -123; // int는 int256과 동일하다.

    // int 타입의 최소값과 최대값
    int256 public minInt = type(int256).min;
    int256 public maxInt = type(int256).max;

    address public addr = 0xCA35b7d915458EF540aDe6068dFe2F44E8fa733c;

    /*
    Solidity에서 byte 타입은 바이트의 시퀀스를 나타낸다.
    Solidity는 두 가지 타입의 바이트 배열을 제공한다.

     - 고정 크기 바이트 배열
     - 동적 크기 바이트 배열
     
 
    bytes1 public a = 0xb5; //  [10110101]
    bytes1 public b = 0x56; //  [01010110]

    // 기본값
    // 초기화되지 않은 변수는 기본값을 가진다.
    bool public defaultBoo; // false
    uint256 public defaultUint; // 0
    int256 public defaultInt; // 0
    address public defaultAddr; // 0x0000000000000000000000000000000000000000
}
```

==Solidity에서 bytes는 동적 크기 바이트 배열을 나타내며, byte[]의 축약형이다.
==


# Constant / Immutable


solidity에서 상수를 선언하는 방법은 `constant`, `immutable` 두가지가 있다. 이렇게 선언된 두 변수는 컨트랙트가 생성된 이후 수정이 불가능하며, 저장 슬롯을 사용하지 않아 가스비용이 낮다. 

## Constant
**컴파일 시점에 고정**된다.  
- 선언 시 바로 값을 할당해야 한다.  
- 초기화 값은 리터럴이어야 한다. 예를 들어, 숫자, 문자열, 주소 등을 직접 입력해야 한다.  
- 컴파일러가 변수의 값을 코드 내 **모든 참조 위치에 복사**하여 사용한다.  
-> 직접 **하드코딩** 되어있어 런타임에 접근비용 거의 들지 X

## Immutable
컨트랙트 생성 시점(constructor) 또는 선언 시에 할당될 수 있다. 한번 설정된 후에는 변경할 수 없다. 
- 선언할 때 초기화하지 않아도 된다. 대신, constructor에서 값을 설정할 수 있다.
- 초기화 값은 동적일 수 있다. 예를 들어, constructor의 매개변수로 전달받은 값을 사용하여 초기화할 수 있다.
- 할당된 이후에는 읽기 전용으로 사용된다. 
- 생성 시점에 한 번 평가된 후, 컨트랙트 런타임 코드에 값이 복사된다. 모든 참조 위치에 값을 복사하며 항상 32바이트다.  
-> 스토리지 접근 X, **런타임 코드 내에서 메모리 슬롯**을 통해 참조되므로 가스비용이 낮아짐. (그래도 여전히 constant보단 비쌈)

> Constant: 컴파일 시점에서 변하지 않는 값을 정의할 때 사용.  
Immutable: 컨트랙트 생성 시 환경에 따라 값이 결정되며, 이후 변경되지 않는 값을 정의할 때 사용.

---

### 예제코드
### Constant

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract Constants {
    address public constant MY_ADDRESS =
        0x777788889999AaAAbBbbCcccddDdeeeEfFFfCcCc;
    uint256 public constant MY_UINT = 123;
}
```
`MY_ADDRESS`, `MY_UINT`
`constant` 로 선언된 이 변수들은 컴파일 시점에 초기화 되고, 변경할 수 없음

### Immutable
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract Immutable {
    address public immutable MY_ADDRESS;
    uint256 public immutable MY_UINT;

    constructor(uint256 _myUint) {
        MY_ADDRESS = msg.sender;
        MY_UINT = _myUint;
    }
}
```

`MY_ADDRESS` `MY_UINT` 변수는 constructor에서 한 번 설정된 수 변경할 수 없음 