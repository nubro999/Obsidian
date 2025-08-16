
|Sui 용어|한글 요약|다른 체인/언어 유사 개념|
|---|---|---|
|Transaction Digest|트랜잭션 해시 식별자|tx hash(Ethereum)|
|Effects|실행 결과 객체 변경 집합|Receipt + state diff 개념적 결합|
|Object|개별 상태 단위(소유/버전)|Solana account / NFT 객체|
|UID|고유 ID 핸들|Primary key|
|Owned Object|특정 주소 소유|ERC-721 token owner|
|Shared Object|다중 접근 전역 객체|Global singleton contract storage|
|Immutable Object|변경 불가 상태|상수 컨트랙트 코드/데이터|
|Coin Object|숫자 값 + type|ERC-20 balance (하지만 분할 coin UTXO 비슷)|
|Programmable Tx Block|다중 명령 배치|Multicall / batch transaction|
|&T / &mut T|불변/가변 참조|Rust borrow / C++ const T& / T&|
|ability key/store/copy/drop|메모리/저장/소유 규칙|Rust trait + ownership 제약 유사|
|Checkpoint|주기적 확정 묶음|블록(유사) / Finality batch|
|Gas Budget|허용 gas 상한|Gas limit (Ethereum)|
|Dynamic Field / Dynamic Object Field|런타임 확장 키-값 부착|Solidity mapping / account data map|
|Event|구조화된 로그|EVM event(log)|