<!-- TITLE: Setting Up The Truffle Vue Box -->
<!-- SUBTITLE: A quick summary of Setting Up The Truffle Vue Box -->

## Summary of Truffle Boxes

Although the truffle boxes, eth-vue and etherplate, looked amazing, setting up those boxes were difficult because of webpack dependencies and unstability of the solidity compilier. I decided to go with the truffle-vue box, which is lightweight and has a basic auth system (examine later).


## Setting up the  Truffle-Vue Box
1.  Setting up the continuous integration (later continuous deployment) was challenging because a local blockchain needs to run in the background, difficulties running a selenium server in `travis.yml`, and unfamiliarity with surge (front-end deployment site).
2.   The links I used were [Selenium server inside travis](https://flatmap.it/2017/11/16/starting-selenium-server-inside-travis/.), the truffle box-ci source code and my own experience setting up pipelines for ENGR 003. Now the truffle box ci, used a similar command I have seen when calling `screen` for another user. `> /dev/null &`. I think that cancels the output or something like that.
3.   After that task was complete, I looked into deploying the application using infura and how to config a wallet to allow users to sign transactions. Installing the `dotenv` on the project allowed me to store sensitive environment variables in a .env file.
 This required me to create a `.env` file containing the mnemonic I wanted to use, and an INFURA api key, obtained by registering for the service. In addition, the truffle configuration file `truffle.js` has to have networks pointing to the designated infura address. First iteration of app can be viewed at [random name](http://gentle-meeting.surge.sh/#/).

```.env
HDWALLET_MNEMONIC="world dune exercise spike now clap night vacant dad fog off special"
INFURA_API_KEY='J0iUetUNOiLgdcX02CGi'
```

<p style="text-align: center">Sample enviroment file, api_key refers to uvic email address</p>

```js
ropsten: {
      provider: new HDWalletProvider(process.env.MNENOMIC, "https://ropsten.infura.io/" + process.env.INFURA_API_KEY),
      network_id: 3,
      gas: 3000000,
      gasPrice: 21
    },
rinkeby: {
			provider: new HDWalletProvider(mnemonic, "https://rinkeby.infura.io/" + process.env.INFURA_API_KEY),
			network_id: 4,
			gas: 4612388,
			gasPrice: 100000000000
}
```

<p style="text-align: center">Corresponding network settings in <pre>truffle.js</pre></p>
See the offical truffle docs for [more info](https://truffleframework.com/tutorials/using-infura-custom-provider), and 
In the end, I decided to use the truffle-vue box, partly because it worked when I installed it, and prefer to move away from react for long-time reasons.
 
Using webpack and surge, I can deploy blockchain applications to surge, directly to the internet.

Webpack is module bundler which takes modules with dependencies and generates static assets representing those modules. In other words, perfect to use on surge.