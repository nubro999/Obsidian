

## 1. **module.exports란?**

- `module.exports`는 Node.js에서 **모듈(파일) 밖으로 함수나 객체를 내보낼 때** 사용하는 문법입니다.
- Truffle에서 마이그레이션 파일(예: `2_deploy_contracts.js`)은 항상 **함수**를 `module.exports`로 내보냅니다.
- Truffle이 이 파일을 실행할 때, 이 함수를 자동으로 호출합니다.

---

## 2. **function(deployer) { ... }의 의미**

- 이 함수는 **Truffle이 마이그레이션을 실행할 때** 자동으로 호출됩니다.
- Truffle이 **`deployer` 객체**를 인자로 넣어줍니다.

---

## 3. **deployer 객체란?**

- `deployer`는 Truffle에서 **스마트 컨트랙트를 배포(deploy)하거나, 여러 작업을 순차적으로 실행**할 수 있게 도와주는 객체입니다.
- 대표적인 메서드:
  - `deployer.deploy(Contract, ...args)` : 스마트 컨트랙트를 배포합니다.
  - `deployer.then(async () => { ... })` : 비동기 작업을 순차적으로 실행할 때 사용합니다.

---

## 4. **실제 동작 예시**

```js
const HelloWorld = artifacts.require("HelloWorld");

module.exports = function(deployer) {
  // deployer 객체를 이용해 HelloWorld 컨트랙트를 배포
  deployer.deploy(HelloWorld);
};
```

- Truffle이 이 파일을 읽고, `function(deployer) { ... }`를 실행합니다.
- 이때 `deployer.deploy(HelloWorld);`가 실행되어, HelloWorld 컨트랙트가 배포됩니다.

---

## 5. **왜 이렇게 쓰는가?**

- Truffle은 여러 컨트랙트/마이그레이션을 **순차적으로** 배포·설정할 수 있어야 합니다.
- `deployer`를 통해 여러 배포 작업을 **체인(연결)**해서 실행할 수 있습니다.
- 예를 들어, 여러 컨트랙트를 배포하거나, 컨트랙트에 초기값을 넣는 작업 등을 순서대로 실행할 수 있습니다.

---

## 6. **정리**

- `module.exports = function(deployer) { ... }`  
  → Truffle이 자동으로 실행하는, **배포(마이그레이션) 작업을 정의하는 함수**입니다.
- `deployer`는 **배포를 도와주는 도구**입니다.
- 이 패턴 덕분에 Truffle은 다양한 배포 시나리오를 유연하게 처리할 수 있습니다.

[[Project Review]]
