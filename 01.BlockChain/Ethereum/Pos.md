https://ethereum.org/ko/developers/docs/consensus-mechanisms/pos/

Proof-of-stake (PoS) underlies Ethereum's [consensus mechanism](https://ethereum.org/ko/developers/docs/consensus-mechanisms/). Ethereum switched on its proof-of-stake mechanism in 2022 because it is more secure, less energy-intensive, and better for implementing new scaling solutions compared to the previous [proof-of-work](https://ethereum.org/ko/developers/docs/consensus-mechanisms/pow/) architecture.

To participate as a validator, a user must deposit 32 ETH into the deposit contract and run three separate pieces of software: an execution client, a consensus client, and a validator client. On depositing their ETH, the user joins an activation queue that limits the rate of new validators joining the network. Once activated, validators receive new blocks from peers on the Ethereum network. The transactions delivered in the block are re-executed to check that the proposed changes to Ethereum's state are valid, and the block signature is checked. The validator then sends a vote (called an attestation) in favor of that block across the network.

Whereas under proof-of-work, the timing of blocks is determined by the mining difficulty, in proof-of-stake, the tempo is fixed. Time in proof-of-stake Ethereum is divided into slots (12 seconds) and epochs (32 slots). One validator is randomly selected to be a block proposer in every slot. This validator is responsible for creating a new block and sending it out to other nodes on the network. Also in every slot, a committee of validators is randomly chosen, whose votes are used to determine the validity of the block being proposed. Dividing the validator set up into committees is important for keeping the network load manageable. Committees divide up the validator set so that every active validator attests in every epoch, but not in every slot.

"위원회(committees)는 검증자 집합(validator set)을 나누어서, 모든 활성 검증자(active validator)가 **모든 에포크(epoch)마다** attest(서명/인증)하지만, **모든 슬롯(slot)마다** attest하지는 않도록 한다."
### 용어 풀이

- **Committee(위원회):** 블록체인(특히 이더리움 2.0)에서 검증자들을 소규모 그룹으로 나눈 것.
- **Validator(검증자):** 블록이나 트랜잭션의 유효성을 확인하고 attest(인증)하는 역할을 하는 노드.
- **Epoch(에포크):** 여러 개의 슬롯으로 구성된 시간 단위(예: 이더리움2.0에서 1 epoch = 32 slots).
- **Slot(슬롯):** 블록이 생성될 수 있는 짧은 시간 단위(예: 12초).
- **Attest(인증):** 검증자가 해당 슬롯의 블록이 유효하다고 투표하는 행위.

지분 증명(Proof-of-Stake)은 검증자들이 네트워크에 자신의 지분을 예치하여 검증자로서의 자격을 얻고, 부정직하게 행동할 경우 그 지분을 잃을 수 있는 위험을 감수하는 방식입니다. 이더리움의 지분 증명에서는 검증자들이 ETH를 스마트 계약에 스테이킹합니다. 검증자는 네트워크에 전파되는 새로운 블록이 유효한지 확인하고, 새로운 블록을 생성하여 전파하는 역할을 합니다. 만약 검증자가 네트워크를 속이려 한다면(예를 들어, 한 번에 여러 블록을 제안하거나 상충되는 인증을 보내는 경우), 스테이킹한 ETH의 일부 또는 전부가 몰수될 수 있습니다.

검증자로 참여하기 위해 사용자는 최소한 32 ETH를 deposit contract에 입금하고, 실행 클라이언트 (execution client), 합의 클라이언트 (consensus client), 검증자 클라이언트(validator client)라는 세 가지 소프트웨어를 실행해야 합니다. ETH를 예치한 후, 사용자는 네트워크에 새로운 검증자가 합류하는 비율을 제한하는 활성화 대기열(activation queue)에 들어갑니다. 활성화된 검증자는 이더리움 네트워크의 다른 peer로부터 새로운 블록을 받습니다. 검증자는 블록에 포함된 트랜잭션을 다시 실행하여 peer로부터 제안된 상태 변경이 유효한지 확인합니다. 새로 제안된 블록이 유효하다고 검증되면, 해당 블록을 지지한다는 투표(인증)를 네트워크에 전파합니다.

![[Pasted image 20250716230345.png]]![[Pasted image 20250716230641.png]]