
# Basic setting
- - **`node_modules/`:** 이 폴더 안에 Hardhat 자체와 Hardhat이 사용하는 모든 JavaScript/TypeScript 라이브러리 (예: Ethers.js, Chai, Mocha 등)가 설치됩니다. Hardhat은 이 폴더 안의 `hardhat` 서브폴더에 위치합니다.
        
        - 예시: `C:\Users\YourUser\Documents\my-web3-project\node_modules\hardhat`
            
    - **`contracts/`:** 여러분이 작성하는 Solidity 스마트 컨트랙트 파일 (`.sol`)들이 저장됩니다.
        
        - 예시: `C:\Users\YourUser\Documents\my-web3-project\contracts\MyContract.sol`
            
    - **`scripts/`:** 배포, 상호작용 등 스크립트 파일 (`.js` 또는 `.ts`)들이 저장됩니다.
        
        - 예시: `C:\Users\YourUser\Documents\my-web3-project\scripts\deploy.js`
            
    - **`test/`:** 컨트랙트 테스트 파일 (`.js` 또는 `.ts`)들이 저장됩니다.
        
        - 예시: `C:\Users\YourUser\Documents\my-web3-project\test\MyContract.test.js`
            
    - **`hardhat.config.js` (또는 `.ts`):** Hardhat 프로젝트 설정 파일입니다.
        
        - 예시: `C:\Users\YourUser\Documents\my-web3-project\hardhat.config.js`
            
    - **`package.json`:** 프로젝트의 종속성 (Hardhat 포함) 및 스크립트가 정의된 파일입니다.
        
    - **`package-lock.json` 또는 `yarn.lock`:** 설치된 패키지들의 정확한 버전 정보가 담긴 파일입니다.
        
    - **`artifacts/`:** Hardhat이 컨트랙트를 컴파일한 후 생성되는 바이너리 코드(bytecode) 및 ABI 파일이 저장됩니다. 이 폴더는 Hardhat이 자동으로 생성합니다.
        
        - 예시: `C:\Users\YourUser\Documents\my-web3-project\artifacts\contracts\MyContract.sol\MyContract.json`
            
    - **`cache/`:** Hardhat 내부 캐싱을 위한 파일들이 저장됩니다. 이 폴더도 자동으로 생성됩니다.
        

**핵심:** Hardhat 개발의 대부분은 `npx hardhat` 명령어를 통해 실행됩니다. `npx`는 현재 프로젝트의 `node_modules/.bin` 경로에서 실행 파일을 찾아주기 때문에, Hardhat을 전역으로 설치할 필요 없이 프로젝트별로 독립적인 환경을 유지할 수 있게 해줍니다.