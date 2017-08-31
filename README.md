# Ethereum Simple Token Smart Contract.

Getting familiar with Ethereum, Smart contracts, Solidity, and the EVM. 

The owner of this contract is allocated a balance of 1000 XYZ. The owner can transfer XYZ to different accounts or fetch his current balance.
User accounts are only able to fetch their current balance. 

### Requirements:

- testRPC - https://github.com/ethereumjs/testrpc                                                                                     
- truffle - https://github.com/trufflesuite/truffle

### Setup:

1. Start testRPC - `testrpc`
2. `cd` into the cloned directory.
3. Compile and migrate the HelloWorld.sol contract. - `truffle compile && truffle migrate --reset`

### Interacting with the contract:

1. All interaction will be done through the truffle console - `truffle console`.
2. Set up the accounts. By default, you are the owner account.
```
truffle(development)> owner = web3.eth.accounts[0]
'0x3192e206552ae569189a49f761b894e82614b638'
truffle(development)> user = web3.eth.accounts[1]
'0x8ecf0a7ca3f4c39bffb6a6a10456681a7dc6260c'
```            
3. Fetch the owner balance. The owner starts with 1000 XYZ funds available.
```
truffle(development)> HelloWorld.deployed().then(a => (a.getBalance(owner).then(console.log)))
{ [String: '1000'] s: 1, e: 3, c: [ 1000 ] }
```
4. Fetch the user balance. The user starts with 0 XYZ funds available. 
```
truffle(development)> HelloWorld.deployed().then(a => (a.getBalance(user).then(console.log)))
{ [String: '0'] s: 1, e: 0, c: [ 0 ] }
```
5. Transfer 25 XYZ from the owner to the user. This creates the following transaction receipt.
```
truffle(development)> HelloWorld.deployed().then(a => (a.transfer(user,25).then(console.log)))
{ tx: '0x2ff5c3b9f9a9b851e0157979533b673b53aaa550c86f10d14c14659b875abc2e',
  receipt:
   { transactionHash: '0x2ff5c3b9f9a9b851e0157979533b673b53aaa550c86f10d14c14659b875abc2e',
     transactionIndex: 0,
     blockHash: '0x9e8633b188178f2a7c879c7ed92847b5eed3f37089c53e4d381c8ad43ea63d0f',
     blockNumber: 5,
     gasUsed: 49166,
     cumulativeGasUsed: 49166,
     contractAddress: null,
     logs: [] },
  logs: [] }
```
6. Re-check user balance. There are now 25 XYZ funds available to the user.
```
truffle(development)> HelloWorld.deployed().then(a => (a.getBalance(user).then(console.log)))
{ [String: '25'] s: 1, e: 1, c: [ 25 ] }
```


