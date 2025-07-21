# 새 폴더 생성 및 이동
mkdir my-hardhat-project
cd my-hardhat-project

# Node.js 프로젝트 초기화
npm init -y

# Hardhat 설치
npm install --save-dev hardhat

-> typescript로 셋팅 -> Hello.sol 작성

==npx hardhat==

```solidity
pragma solidity ^0.8.0;

contract Hello {
    string public greet = "Hello, Hardhat!";
}
```

```
Generating typings for: 2 artifacts in dir: typechain-types for target: ethers-v6
Successfully generated 8 typings!
Compiled 2 Solidity files successfully (evm target: paris).
```
이게 무슨 뜻이지?

-> ==npx hardhat test==

- In Solidity, a `public` variable creates a getter function, but in JavaScript/ethers.js, you should call it as a property, not as a function.
- 이 문제로 테스트가 실패함, public으로 선언하면 getter가 자동생성되는데 js에서는 함수로 호출하면 안됨
--응 아니고 deployed() 함수가 없어져서 에러남, 사용하지 말것


## scripts/deploy.ts
```solidity
const Hello = await ethers.getContractFactory("Hello");
const hello = await Hello.deploy();
// ethers v6에서는 await hello.deployed() 필요 없음
console.log("Hello deployed to:", hello.target); // v6에서는 .address 대신 .target
```

-> ==npx hardhat node==

-> ==npx hardhat run scripts/deploy.ts --network localhost==

```ts
async function call() {

    const [owner, addr1, addr2] = await ethers.getSigners();


  const contractAddress = "0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512"; // 실제 배포된 주소

  const Hello = await ethers.getContractFactory("Hello");

  const hello = Hello.attach(contractAddress).connect(addr1); // 연결된 계약 인스턴스 생성
  // 함수 호출
  const greeting = await hello.greet();

  console.log("greeting:", greeting);

  console.log("call contract address:", hello.target);

  console.log("called by:", addr1.getAddress());

}
call();
```
이런 식으로 다른 주소에서 배포된 컨트랙트 호출가능


# nest-pj

이제 nest.js 로 프론트엔드 제작
nest-pj파일을 만들고(nest new nest-pj)

npm run start:dev
![[Pasted image 20250721184510.png]]
등장

모듈 만들기
nest g module contract
nest g controller contract
nest g service contract

추가 라이브러리
npm install ethers


```ts
@Controller('contract') // 엔드포인트의 기본 경로: /contract
export class ContractController {
  constructor(private readonly contractService: ContractService) {}

  @Get('greeting') // GET /contract/greeting 엔드포인트 생성
  async getGreeting() {
    const greeting = await this.contractService.getGreeting();
    return { greeting };
  }
}
```
여기서 엔드포인트가 만들어짐

-> 이제 다시 hardhat에 네트워크를 실행 -> 컨트랙트배포하고
-> localhost:3000/contract/greeting을 입력

![[Pasted image 20250721191134.png]]
성공! 컨트랙의 함수를 호출하여 값을 받아옴


