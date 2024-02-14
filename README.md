# Blockchain-Developer-Interview-Questions-and-Answers

If I was a hiring manager?
Have a look at some of the EIP. What they will be asking is most likely some depth questions such as difference between call data and memory and other stuff. All the best.



Some basic questions related to blockchain like what are nodes, blocks, transactions etc.

How DeFi works and some examples of DeFi projects: I explained basic DeFi architecture, AMM and some mathematical concepts working behind the scenes like constant multiplication formula.

What are Zk-SNARKS? Difference between optimistic rollups and zk rollups. : I explained most of things at engineering level.

what you have learned so far and why would you like to join the internship program? : Be genuine and dont fake anything.

Few general questions were there related to latest happening in blockchain space like DAO, NFTs, MEV, flashloans.
What Zero-knowledge application do I hope to see.

What ETH2 is all about. Had to explain PoS and a couple of stuff.

My knowledge of what Nethermind does.

My interests

Had a couple of personal projects in my resume. So, I was asked to explain one of them from scratch and how I went about implementing it.
How did the DAO hack happen? How can you avoid doing the same thing in your contract?

eentry using a proxy contract where the default payable fallback recalls the withdraw function.

Solve it by updating balances before executing the withdraw and checking the return values of ether transfer. Use transfer over send, as transfer reverts.

I believe it’s also advised to use transfer over other functions to transact

There are some dangers in using send: The transfer fails if the call stack depth is at 1024 (this can always be forced by the caller) and it also fails if the recipient runs out of gas. So in order to make safe Ether transfers, always check the return value of send, use transfer or even better: Use a pattern where the recipient withdraws the money.
What is the stack depth? What is the maximum number of stack items you can access in a single operation? Explain, in detail, the difference between memory and the stack?

What is the difference between Call, Saticcall and DelegateCall?
What is the most gas-efficient way to store data?

What is Parity Wallet lock?

Explain elliptic curve key pairs?
Explain how a contract can be upgraded after deployed? Read upgradable section in Open Zeppelin docs

What are all the function access modifiers? search solidity docs in functions section

When should you emit events? when the state changes in a way that would be helpful to track offchain

What's the most gas efficient way to implement double value mapping? hash the two variables together and use that as a key in the mapping

What's 1 common security pitfall and how to avoid it? this is pretty open ended, but start with re-entrency probably.

If you want to multiply by a decimal how is that implemented using uints? say you want multiple 10,000 by 0.05. This is the same as 10000 * 5 / 100

What's the largest and smallest uint sizes? uint8, uint256
https://dzone.com/articles/how-to-pass-interview-on-solidity-part-1



Calling each function, we can see that the public function uses 496 gas, while the external function uses only 261.

The difference is because in public functions, Solidity immediately copies array arguments to memory, while external functions can read directly from calldata. Memory allocation is expensive, whereas reading from calldata is cheap.

The reason that public functions need to write all of the arguments to memory is that public functions may be called internally, which is actually an entirely different process than external calls. Internal calls are executed via jumps in the code, and array arguments are passed internally by pointers to memory. Thus, when the compiler generates the code for an internal function, that function expects its arguments to be located in memory.

For external functions, the compiler doesn't need to allow internal calls, and so it allows arguments to be read directly from calldata, saving the copying step.

As for best practices, you should use external if you expect that the function will only ever be called externally, and use public if you need to call the function internally. It almost never makes sense to use the this.f() pattern, as this requires a real CALL to be executed, which is expensive. Also, passing arrays via this method would be far more expensive than passing them internally.

You will essentially see performance benefits with external any time you are only calling a function externally, and passing in a lot of calldata (eg, large arrays).

Examples to differentiate:

public - all can access

external - Cannot be accessed internally, only externally

internal - only this contract and contracts deriving from it can access

private - can be accessed only from this contract
Share
Improve this answer
I'd question their theoretical knowledge about blockchains, asymmetric encryption, signatures, why are transactions atomic, stack-based virtual machines, data types in Solidity and why is uint256 more efficient, inheritance, popular interfaces (openzeppelin standards), tx.origin vs msg.sender, reentrancy attacks...really just go and see how deep they are in the field and are they aware of how robust the code has to be in dapps.
Then I'd ask to see some real-world things they built, explain what problems they solved and what steps they took to reach the solution; what were the critical points, what tools and frameworks they used and what they would like to work on in the future.
Good luck!


I've only done one interview, but they asked for:
Identifying smart contract bugs
Unconventional reentrancy attacks
Gas optimization

What specific knowledge prerequisites do interviewers seek for from the candidates?
I'd want:
Experience with smart contract development across a couple of major frameworks (foundry and hardhat probably the most relevant now, but ape-safe/brownie would be fine too and is very relevant for vyper apps), truffle is also fine but I don't see it so often these days.
In particular, good grasp of testing and deployment is really important. You need to know not just how to write unit tests, but how to run tests and deployments locally, against network forks and, ideally, using some techniques like fuzzing and invariant testing.
I'd want a candidate to be well-versed in AT LEAST solidity and Typescript. A background in web development (server and client side) would be super useful based on the nature of web3 apps, if you're on the research side, math, engineering or compsci would be great.
I'd also really appreciate some domain knowledge: i.e: some kind of finance or trading chops if working in DeFi, passion for gaming if working in gaming, experience with computer science or a real passion for it if building infra. We do DeFi, so if you are well-versed in the DeFi landscape that's a big plus.

I haven't mentioned solidity yet because it's honestly...not that hard a language. It's also hard to do really creative things with it because of the gas constraints of the EVM. That said:
At a basic level you should be familiar with solidity syntax for v8 and v7 pragmas at least. Couple of basic things that jump to mind:
Types
Storage vs memory vs calldata
Public private internal external
Inheritance and use of libraries
Loops and breaks
Gas costs and the biggest gas operations
Understanding of basic ERC standards (20, 721, 1155 etc)
Basic syntax (variables, functions, inheritance, modifiers, structs)
The ABI as a JSON object and abi methods for encoding/decoding data
Low level calls and transfer syntax, along with difficulties of each
Constants and immutables
Really though, I'm looking for someone who has a solid understanding of the EVM as it relates to deploying smart contracts. In particular:
EVM storage and memory layouts
Understanding contract bytecode: i.e. function selectors and structure of a function call in bytecode
Mapping of gas to major opcodes (SSTORE, SLOAD (and warm SLOAD), MLOAD etc etc)
Slot packing
Variable vs dynamic arrays and mappings, and when to use each
Upgradeable contracts and proxies
EOAs vs smart contract accounts in the ethereum state model
Basic understanding of the challenges of MEV for users and developers
Major known exploits and how to avoid them (reentrancy, untrusted calls, etc etc)

 The questions usually revolve around project experience, much like DeFi economic models (Compound, Uniswap V1/V2/V3), gas optimization, and the EVM. However, if you are interviewing a blockchain developer rather than a smart contract developer, consensus algorithms and network-related topics are likely to be more important.

 Gas optimization is the most frequently asked topics in my interviews..The answer can be very extensive, covering everthing in evm from storage to calling procedures.so you can talk more about what you are familiar with.
And the models of uniswap v1/v2 is also frequent. All my interviews teams were Chinese or Hong Kong componies, there is no leetcode test.

Being aware of the kind of security issues you can encounter when using diamond/upgradeable patterns or deploying contracts using the ‘create2’ OPCODE; being able to explain how it works at a high level; that’s the kind of knowledge an employer should seek imho.
've seen algos in the wild in a few places (OZ Governor for example), and an appreciation for the distinction between arrays and hashmaps is pretty fundamental to solidity programming. Merkle trees come up a lot, as a core data structure of the Ethereum state.
RareSkills has some good ones you can practice with. Google it
It was a pretty technical conversation where he really tried to challenge me about my knowledge of the ethereum protocol. Know that they are mostly about ethereum RFCs and EIPs and protocol engineering.
R3: Take home assignment, just a path finding problem using Djikstras. Took 1 hour.
What is the biggest codebase you’ve worked in, by code volume and team size. A scan through your github profile (tests are a plus). How detail oriented you are around security and common blockchain bugs/vulnerabilities. Finally, I will ask about things that are specific to the project, such as implementations for upgradable contracts, addressing contract storage slots, delegated calls, packing binary, and optimizing gas, storage, and compute complexity.
I got one: How many bytes does EVM use to store data?
How did the DAO hack happen? How can you avoid doing the same thing in your contract?Reentry using a proxy contract where the default payable fallback recalls the withdraw function.
Solve it by updating balances before executing the withdraw and checking the return values of ether transfer. Use transfer over send, as transfer reverts.
I believe it’s also advised to use transfer over other functions to transact
There are some dangers in using send: The transfer fails if the call stack depth is at 1024 (this can always be forced by the caller) and it also fails if the recipient runs out of gas. So in order to make safe Ether transfers, always check the return value of send, use transfer or even better: Use a pattern where the recipient withdraws the money.

What are the 4 function access modifiers in solidity?Public private internal external?

What is the stack depth? What is the maximum number of stack items you can access in a single operation? Explain, in detail, the difference between memory and the stack?
What is the difference between Call, Saticcall and DelegateCall?
What is the most gas-efficient way to store data?ie, storing data in structs is more efficient. Also uint8 consumes the same space as uint256, but unit8 array consumes less than uint256 array
What is Parity Wallet lock?
Explain elliptic curve key pairs?
Differences and similarities of erc20 and erc721
xplain how a contract can be upgraded after deployed? Read upgradable section in Open Zeppelin docs
What are all the function access modifiers? search solidity docs in functions section
When should you emit events? when the state changes in a way that would be helpful to track offchain
What's the most gas efficient way to implement double value mapping? hash the two variables together and use that as a key in the mapping
What's 1 common security pitfall and how to avoid it? this is pretty open ended, but start with re-entrency probably.
If you want to multiply by a decimal how is that implemented using uints? say you want multiple 10,000 by 0.05. This is the same as 10000 * 5 / 100
What's the largest and smallest uint sizes? uint8, uint256
Another upgrade option is the diamond standard https://eips.ethereum.org/EIPS/eip-2535
Most interviews will have you create some sort of implementation of a basic functionality for example create a mini ERC20 staking contract or a mini opensea, or a mini DAO, etc. They also want to make sure you understand the caveats of the language and how to resolve them.
Also the basics of when to use things like internal, external, pure, payable etc. What does unchecked do? Spot the underflow/overflow risk. Many possible ways they can go
Blockchain And Blockchain Alternatives

What is a blockchain?
A blockchain is a digital file consisting of records. The number of records is growing in regular blocks of time. All records are linked together using cryptography
For a blockchain to be decentralised it has to be distributed to a group of people
Why are blockchains resistant to modification of their data?
Because once recorded, the data in any given block cannot be altered retroactively without altering all subsequent blocks
Tell me the three factors of the blockchain trilemma?
security, decentralization, and scalability -> you can only choose two!
What problem does a blockchain solve?
How can I save a digital information in a immutable way without a centralised authority
Explain a blockchain alternative
Transactions in a Directed Acyclic Graph (DAG) are linked to one and another directly instead of being grouped and processed in blocks. This makes DAGs more scalable than blockchains in theory
Can you “hide” a transaction on a blockchain?
Transaction can't be hidden. All transactions are public
Where are transactions stored in a blockchain?
In a blockchain, a transaction is stored in a "block"
This blocks are saved on nodes that are part of the network
What is a miner?
Miners are nodes, who receive rewards for verifying transactions and marinating network integrity
What is a hard fork?
Hard forks are protocol changes which aren't compatible with the older version of the cryptocurrency. The chain splits into two and the participants can choose to operate in any version
Immediately after a blockchain forks, the two resulting chains share the exact same transaction history
What is a soft fork?
In contrast to a hard fork, soft forks are backward compatible. They don’t have a significant impact on the change of protocol and participants can operate within the network without upgrading their software
How does Proof of Work work?
The central principle behind PoW consensus is to solve a complex mathematical problem. The first miner to find the right solution, advertise it to the whole network, and receive a reward in cryptocurrency provided by the protocol
The disadvantage is that it requires a lot of computational power
How does Proof of Stake work?
It is a cryptocurrency consensus mechanism
Proof of Stake tries to deal with the main drawback of PoW
The central principle behind PoS consensus is that cryptocurrency owners can stake their crypto. From this so called "validators" one then is selected randomly to "mint" a new block. The more coins a person stakes, the higher is the chance to be selected
What is a proof of work nonce?
A nonce plays a crucial part in the mining process with PoW. The nonce is the missing piece of the puzzle needed to discover the next block
What does "nonce" mean?
"nonce" stands for "Number User Only Once"
Cryptography

What is a hash collision?
A hash collision occurs, if two different inputs lead to the same hash
What is symmetric key encryption?
Symmetric key encryption is also called private key cryptography and uses the same key to encrypt and decrypt messages
What is asymmetric key encryption?
Symmetric key encryption is also called public key cryptography and uses two separate keys to encrypt and decrypt messages
First a private key is randomly generated. With the use of a mathematical formula the public key can be created from the private key. The public key can be shared with everyone, whereas the private key must be kept secret
Data is encrypted using any one of the keys and decrypted with the other. Unlike with symmetric encryption only the encrypted data (but not the key itself) has to be transferred, making it more secure against man-in-the-middle attacks
What is a merkle tree?
A merkle tree is a data structure used to efficiently summarize and validate large data sets
A merkle tree consists of the merkle root, which is the root hash. The merkle root is then put into the block header of a block
In a merkle tree, the the transaction hashes are considered the leaves. Each non-leaf node (branch) is a hash of its child hashes
Why are merkle trees so important in BTC?
If Bitcoin didn’t have merkle trees, every node on the network would need to maintain a full copy of every transaction that has ever happened in Bitcoin
Explain the term "zero knowledge proof"
It is a cryptographic method that allows one party to prove the knowledge of certain information to the other party without revealing the data in question
Attacks

What is a 51% attack?
If a hacker is able to control 51% or more of the nodes, he will gain control over the entire network
What is a reentrancy attack?
A reentrancy attack occurs when a function makes an external call to an untrusted contract. The untrusted contract then makes a recursive call back to the original function in an attempt to drain funds
Name two ways reentrancy attacks can be prevented
Implementing the checks-effects-interactions pattern (update the state before making external calls)
Using a reentrancy guard (e.g modifier by OpenZeppelin)
What is a replay attack?
A replay attack is taking a transaction on one blockchain, and maliciously or fraudulently repeating it on another blockchain. Two post-fork blockchains are vulnerable for this type of attack
For a replay attack to work the two chains need to share a common history
How can a blockchain prevent replay attacks?
To prevent replay attacks, the developers on one of the two post-fork blockchains can make a slight change to transaction rules
Ethereum prevents same-chain replay attacks by having a transaction counter in each account. This nonce also prevents double spending
Ethereum

What is Ethereum?
Ethereum is a decentralized, open-source blockchain with smart contract functionality
What is Ether?
Ether is Ethereum’s native cryptocurrency
It provides the nodes an incentive to validate the Ethereum blockchain blocks
List some Ethereum development and testing environments
Truffle
Hardhat
Brownie
How large is the block size of Ethereum?
Ethereum does not have a block size limit; blocks use gas limits
How big is the block reward of Ethereum?
Currently it is 2 ETH. But this number could change in the future
What is the block time of Ethereum?
The average block time is around 13.2 seconds. But this value can fluctuate. Get the current value from here
What is the smallest unit of Ether?
1 Wei (10 ** 18 Wei = 1 Ether)
Bring the denominations in the right order: Gwei, Mwei, Kwei, Ether, Wei, microether, milliether
Wei, Kwei, Mwei, Gwei, microether, milliether, Ether
Who founded Ethereum?
Ethereum was founded by Vitalik Buterin, along with seven other co-founders. One of them is Gavin Wood
When did Ethereum launch?
How does Ethereum differ from Bitcoin?
What are smart contracts?
What is the EVM?
What is Enterprise Ethereum?
What is a node in Ethereum?
A node is a computer connected to the Ethereum network, which is responsible for processing transactions
How can you connect with a node?
You can connect to a node by WS-RPC, JSON-RPC, and IPC-RPC
Which consensus mechanism does Ethereum use?
Ethereum currently uses proof of Work but plans to use proof of stake in Ethereum 2.0
Which programming language is used to write smart contracts in Ethereum?
Solidity is the primary programming language used for writing smart contracts and dApps. Vyper is also used
List common smart contract standards
ERC-20: Token Standard
ERC-165: A standard to publish and detect what interfaces a smart contract implements.
ERC-721: Non-fungible token standard
ERC-1155: Multi-token standard
What is integer underflow/overflow?
Integer overflows and underflows occur due to the input, whose size does not meet the boundaries of integer variables
Hint: To avoid this, simply make sure you’re using a Solidity compiler version > 0.8, which automatically checks for overflows and underflows
What is a frontrunning?
Transactions take some time before they are mined. An attacker can watch the transaction pool and send a transaction, have it included in a block before the original transaction. This mechanism can be abused to re-order transactions to the attacker's advantage
What is the account nonce in Ethereum?
It's the transaction count of an account
It prevents replay attacks
How can you obtain ether?
Ether can be obtained by mining or by trading Ether with other cryptocurrencies
What are the two types of Ethereum networks that exist?
Public networks (Mainnet, test networks: Ropsten, Goerli, Kovan, Rinkeby)
Private networks (Enterprise Ethereum, local networks)
Why are gas fees taken?
The creation of consensus in a decentralised system must cost something, because it motivates all participants to save the optimal reality
How much gas does a simple Ethereum transaction cost?
A simple transfer of value requires 21'000 gas
How many transactions fit into an Ethereum block?
There is no general answer for this, because transactions utilize different amounts of gas and a block has a variable size (depending on network demand)
How are the transaction fees calculated in Ethereum after the London upgrade?
Gas units (limit) * (base fee (in Gwei) + priority fee (tip))
Info: Miners receive the tip and the base fee is burned
Read the docs to find out more about gas
What is an ABI?
ABI is an acronym for Application Binary Interface
The ABI is the interface to interact with our smart contract
The ABI can be generated from your smart contract source code (you have to compile it)
What do I need to interact with a deployed smart contract?
You need the contract address and the ABI
The contract address points to the place where the bytecode is located on the blockchain
The ABI defines which functions you can invoke
How are smart contracts stored into the blockchain?
They are stored as bytecode (=binary data) under a specific address also known as contract address
Solidity

Why should a developer define a solidity version at the beginning of a file?
It reduces incompatibility glitches that can occur while compiling with another version
Why is is hard to generate random numbers in a smart contract?
Solidity contracts are deterministic. Anyone who figures out how your contract produces randomness can anticipate its results and use this information to exploit your application
How can random numbers be generated in a smart contract?
To make random numbers unpredictable you must use an oracle to produce randomness off-chain. A popular way is to use ChainLink VRF
Why do smart contracts written in Solidity or Viper need to be compiled?
The EVM doesn't understand these high-level languages. Therefor the source code has to be translated into machine language (bytecode) that the EVM is able to execute
Explain the naming conventions for contracts and functions in Solidity
Contract names should be capitalised (e.g TestContract)
Function names should be mixed-case (e.g superDuperFunction)
Learn more about the style guide here
Do all functions in a smart contract costs gas?
Functions that modify the state of EVM costs gas, whereas functions that only read the state are free
List all valid data types of Solidity
Boolean, Integer, Address, Byte/String, Enum
The data type "Fixed Point Numbers" also exists, but isn't fully supported yet
What is the result of 7/2 in Solidity?
It is 3 because the decimal gets truncated
What data types are not valid keys in a mapping?
The key can be any built-in data type but reference types are not allowed. Not allowed are: Mapping, Struct, Enum or dynamically sized Array.
What is the advantage of a defining a fallback function in Solidity?
It helps us to protect the function from throwing an error
In which two scenarios a fallback function (defined as payable) gets called in Solidity?
A contract receives only ether and no data (msg.data)
No function name matches the called function
What is special about the fallback function in Solidity?
It has no name, arguments or identifier
It can not return anything
It can only be defined once per contract
It is mandatory to mark it external
It is limited to 2300 gas when called by another function
What is the difference between ERC & EIP?
Ethereum Request for comments (ERC) define standards for the usage of Ethereum
Ethereum Improvement Proposals (EIP) improve the Ethereum protocol itself
Interview Coding Problems (& Solutions)

Compare two strings in Solidity
Hint: You can’t directly compare two strings, but one method would be to hash both strings & compare the hashes.

https://www.rareskills.io/post/solidity-interview-questions
Dutch Auction

The Dutch Auction is a type of reverse auction. The auctioneer starts with a high asking price and gradually lowers it until someone bids. The bidder is the winner.

If something needs to be sold, a price has to be found. Many systems have been created to facilitate price discovery: negotiations, order books, market research and even horoscopes. However, none are as effective at immediate price discovery as auctions. They are the way to facilitate the sale of anything – an artwork, a deed or a right – to the immediate market. 
Their simplicity, effectiveness and power have cemented auctions as a cornerstone of decentralized finance and one auction type is almost universally found among the largest decentralised finance applications: the Dutch Auction. The total duration is known before the auction has begun; it is incredibly effective at price discovery because of its completely transparent and predictable operation; it allows immediate delivery upon payment, and most importantly it allows for the fewest transactions for everybody: 1. Paid by the buyer.
Auction logic
The auction is initiated with a start date, end date and a start price.
The price is always known at any time as the linear line connecting the points:
start date, start price. (startPrice = a · startDate + b)
end date, 0. (0 = a · end date + b)
Once someone bids, they are immediately provided with the assets. In a smart contract, delivery is often provided by a privileged function call on behalf of the contract. 
It is important that the delivery is immediate, as a potential winner might use a flash loan to get the required capital.
Task
Implement the dutch auction in a smart contract language like Anchor, Solidity or Vyper.
If you know Rust, we recommend Anchor. If you know Python, we recommend Vyper.
The smart contract should be covered by tests showcasing how to interact with the smart contract and the described lifetime of the auction. 


(continued on next page)
Testing frameworks for Solidity and Vyper are eth-brownie (python), Truffle (javascript) or Hardhat (javascript). Eth-brownie is recommended, but Truffle and Hardhat are fine.
Anchor contains a truffle-like test suite.

Any library or code snippet released under a permissive license like MIT can be used. If you are uncertain if a code snipped is released under a permissive license, assume it is not.
Tips and tricks
To help people with little to no experience with smart contracts, here are some tips and tricks to improve your smart contract.

Knowing how to use testing frameworks is key to writing secure smart contracts. At Polymer labs 90% of our tests are property based, that means we are testing a variety of random inputs along with inputs that previously failed. This has allowed us to detect many edge cases failures which could otherwise have gone unnoticed. Eth-brownie implements property based testing natively.

Openzeppelin libraries are released under MIT.

What do you get if you divide the integers 7199 by 3600? 
Alt: 2·359953600 · 10= ? 
This is a tip and not a question. But feel free to provide an answer.
