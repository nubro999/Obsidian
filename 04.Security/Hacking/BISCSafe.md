
web3문제

처음으로 풀었는데 아무것도 모르겠다.
metamask연결함
hardhat다운 받음
RemixIDE에서 컴파일해봄

금고주소랑 내 계정 주소, 소유주(owner) 주소 세가지의 주소가 있고
나의 주소로 opensafe()를 콜할 경우 열리지 않음

```cpp
// SPDX-License-Identifier: MIT

pragma solidity >= 0.7.0 < 0.9.0;

  

contract Safe { //컨트랙트이름은 Safe

    address public owner; //소유자 주소를 저장하는 변수

    string private flag =  "bisc2023{FAKE_FLAG}"; //플래그 변수, 실제 플래그는 이와 다름

  

    constructor() { //생성자 함수, 컨트랙트가 배포될 때 실행됨

        owner = msg.sender;

    }

  

    function opensafe() public view returns (string memory) {

        if(owner == msg.sender){

            return flag;

        }

        else {

            return "Your not owner!!";

        }

    }

  

    function changeOwner(address _owner) public { //소유자 주소를 변경하는 함수

        require(owner == msg.sender, "Your not owner!!");

        owner = _owner;

    }

}
```

이게 sol파일

나는 블로그를 보고 web devtool을 사용했는데 어떻게 작동하는 지 잘 모르겠다. 서버랑 작동하는 것 같긴한데..

아직 dev tool의 작동방식을 정확히 모르겠다
그리고 solidity의 언어도 잘 모르겠다
이더리움 파일구조도 모르겠다.