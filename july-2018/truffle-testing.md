<!-- TITLE: Truffle Testing -->
<!-- SUBTITLE: A quick summary of Truffle Testing -->

# Automated tests in truffle

After loading in a contract in truffle migrations using the standard `const token = artifacts.require('./token.sol')`, the test files run in truffle can be executing using either javascript files or solidity files, although my first dapp, a simple token factory will be created using javascript tests, I intend to use solidity files to test my future dapps.

```js
artifacts.new()
artifacts.at(<contract>)
artifacts.deployed()
```

Now, `artifacts.deployed()` uses an existing contract live on the blockchain, usually deployed by truffle migration.

`artifacts.new()` is probably the best for automated tests as it creates a new contract, however this can consume a lot of ether, resulting in misleading deployment costs. For example when I was testing my smart contracts for ENGR 003, I actually ran out of eth a few times.

For dynamically created contracts such as a token factory, using `artifacts.at(<contract>)` makes the most sense, reading in a emitted event parameter (instantation address) and then interacting with that contract is quite valuable for testing.

In addition, solidity files can be used for automated testing, smart contracts testing smart contracts.


