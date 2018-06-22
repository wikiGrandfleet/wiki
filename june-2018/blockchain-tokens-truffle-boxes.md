<!-- TITLE: Blockchain Tokens Truffle Boxes -->
<!-- SUBTITLE: A quick summary of Blockchain Tokens Truffle Boxes -->

#### Tutorials to look at 

1.  [Gluton-Contracts](https://github.com/gluon-project/gluon-contracts/blob/master/contracts/GluonToken.sol)
2.  [etherplate](https://truffleframework.com/boxes/etherplate) In particular focus on ERC 721 Token functionality
3.  [vue-eth](https://truffleframework.com/boxes/eth-vue), i can't believ you can just deploy the box and no worries about anything after.

Spend a few hours with vue-eth and etherplate.

### CI for Truffle projects using gitlab

First create a network that points to the correct docker image pulled from docker hub, [ganache-cli](https://github.com/trufflesuite/ganache-cli), remember to include the service in docker (`gitlab-ci.yml`) for every single job.
```js
test_truffle:
  stage: test
  services:
   - trufflesuite/ganache-cli
  script:
   - npm install truffle
   - ./node_modules/truffle/build/cli.bundled.js compile
   - ./node_modules/truffle/build/cli.bundled.js migrate --network gitlab
   - ./node_modules/truffle/build/cli.bundled.js test --network 
```

And update the corresponding `truffle.js` file.
```js
gitlab: {
      host: "trufflesuite-ganache-cli",
      port: 8545,
      network_id: "*" // Match any network id
  }
```

The full `truffle.js` is listed below, but this is just the boilerplate for a simple truffle box project.
```js
module.exports = {
  // See <http://truffleframework.com/docs/advanced/configuration>
  // for more about customizing your Truffle configuration!
  networks: {
    development: {
      host: "127.0.0.1",
      port: 8545,
      network_id: "*" // Match any network id
    },
    gitlab: {
      host: "trufflesuite-ganache-cli",
      port: 8545,
      network_id: "*" // Match any network id
    }
  }
};
```

The `gitlab-ci.yml` file is fairly simple,  and lightweight using two docker images and having them commmmunication with each other.
```js
image: node:8.1.1

cache:
  paths:
  - node_modules/

stages:
  - test

test_truffle:
  stage: test
  services:
   - trufflesuite/ganache-cli
  script:
   - npm install truffle
   - ./node_modules/truffle/build/cli.bundled.js compile
   - ./node_modules/truffle/build/cli.bundled.js migrate --network gitlab
   - ./node_modules/truffle/build/cli.bundled.js test --network gitlab
```