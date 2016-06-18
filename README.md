# Ethereum blockchain dashboard

This is a simple visualization project for my ApolloChain demo/prototype.

It is based on web3.js and communicates directly with the local Ethereum node running on your machine. You should run your node with parameters like those:

``` sh
geth --networkid 42 --nodiscover --rpc --rpccorsdomain "*" console
```

In order to allow the browser to communicate with the RPC API.

To build the project, run:

``` sh
browserify viz.js -o main.js
```

## Setup

You need to change the `account` variable to your account address, and `contractAddress` to the address of the ApolloTrade smart contract deployed on your blockchain.

If your Ethereum client's RPC port is different than the default, change the following line:

``` javascript
var web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
```

`abi.js` contains the ABI for the smart contract.

## How it works

The web3 API is used to display some information about the account:

- Ether balance
- Current block number

ApolloTrade smart contract functions are called to display specific information:

- ApolloCoin balance
- Energy balance

Then a filter is set up to scan all new blocks for transactions and display their contents.

`getFunctionHashes()` and `findFunctionByHash()` are used to decode the function hash found in the `input` parameter for the transaction. Then, web3's `SolidityCoder` internal class is used to decode the parameters for the function. This allows us to display the details of the ApolloTrade smart contract functions.
