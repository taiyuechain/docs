**Contents**
- [JSON RPC API](#json-rpc-api)
  - [JavaScript API](#javascript-api)
  - [JSON-RPC Endpoint](#json-rpc-endpoint)
    - [Go](#go)
  - [JSON-RPC support](#json-rpc-support)
  - [The default block parameter](#the-default-block-parameter)
  - [Curl Examples Explained](#curl-examples-explained)
  - [JSON-RPC methods](#json-rpc-methods)
  - [JSON RPC API Reference](#json-rpc-api-reference)
      - [web3_clientVersion](#web3_clientversion)
        - [Parameters](#parameters)
        - [Returns](#returns)
        - [Example](#example)
      - [web3_sha3](#web3_sha3)
        - [Parameters](#parameters-1)
        - [Returns](#returns-1)
        - [Example](#example-1)
      - [net_version](#net_version)
        - [Parameters](#parameters-2)
        - [Returns](#returns-2)
        - [Example](#example-2)
      - [net_listening](#net_listening)
        - [Parameters](#parameters-3)
        - [Returns](#returns-3)
        - [Example](#example-3)
      - [net_peerCount](#net_peercount)
        - [Parameters](#parameters-4)
        - [Returns](#returns-4)
        - [Example](#example-4)
      - [yue_protocolVersion](#yue_protocolversion)
        - [Parameters](#parameters-5)
        - [Returns](#returns-5)
        - [Example](#example-5)
      - [yue_syncing](#yue_syncing)
        - [Parameters](#parameters-6)
        - [Returns](#returns-6)
        - [Example](#example-6)
      - [yue_coinbase](#yue_coinbase)
        - [Parameters](#parameters-7)
        - [Returns](#returns-7)
        - [Example](#example-7)
      - [yue_gasPrice](#yue_gasprice)
        - [Parameters](#parameters-10)
        - [Returns](#returns-10)
        - [Example](#example-10)
      - [yue_accounts](#yue_accounts)
        - [Parameters](#parameters-11)
        - [Returns](#returns-11)
        - [Example](#example-11)
      - [yue_blockNumber](#yue_blocknumber)
        - [Parameters](#parameters-12)
        - [Returns](#returns-12)
        - [Example](#example-12)
      - [yue_getBalance](#yue_getbalance)
        - [Parameters](#parameters-13)
        - [Returns](#returns-13)
        - [Example](#example-13)
      - [yue_getStorageAt](#yue_getstorageat)
        - [Parameters](#parameters-14)
        - [Returns](#returns-14)
        - [Example](#example-14)
      - [yue_getTransactionCount](#yue_gettransactioncount)
        - [Parameters](#parameters-15)
        - [Returns](#returns-15)
        - [Example](#example-15)
      - [yue_getBlockTransactionCountByHash](#yue_getblocktransactioncountbyhash)
        - [Parameters](#parameters-16)
        - [Returns](#returns-16)
        - [Example](#example-16)
      - [yue_getBlockTransactionCountByNumber](#yue_getblocktransactioncountbynumber)
        - [Parameters](#parameters-17)
        - [Returns](#returns-17)
        - [Example](#example-17)
      - [yue_getCode](#yue_getcode)
        - [Parameters](#parameters-18)
        - [Returns](#returns-18)
        - [Example](#example-18)
      - [yue_sign](#yue_sign)
        - [Parameters](#parameters-19)
        - [Returns](#returns-19)
        - [Example](#example-19)
      - [yue_sendTransaction](#yue_sendtransaction)
        - [Parameters](#parameters-20)
        - [Returns](#returns-20)
        - [Example](#example-20)
      - [yue_sendRawTransaction](#yue_sendrawtransaction)
        - [Parameters](#parameters-21)
        - [Returns](#returns-21)
        - [Example](#example-21)
      - [yue_call](#yue_call)
        - [Parameters](#parameters-22)
        - [Returns](#returns-22)
        - [Example](#example-22)
      - [yue_estimateGas](#yue_estimategas)
        - [Parameters](#parameters-23)
        - [Returns](#returns-23)
        - [Example](#example-23)
      - [yue_getBlockByHash](#yue_getblockbyhash)
        - [Parameters](#parameters-24)
        - [Returns](#returns-24)
        - [Example](#example-24)
      - [yue_getBlockByNumber](#yue_getblockbynumber)
        - [Parameters](#parameters-25)
        - [Returns](#returns-25)
        - [Example](#example-25)
      - [yue_getTransactionByHash](#yue_gettransactionbyhash)
        - [Parameters](#parameters-26)
        - [Returns](#returns-26)
        - [Example](#example-26)
      - [yue_getTransactionByBlockHashAndIndex](#yue_gettransactionbyblockhashandindex)
        - [Parameters](#parameters-27)
        - [Returns](#returns-27)
        - [Example](#example-27)
      - [yue_getTransactionByBlockNumberAndIndex](#yue_gettransactionbyblocknumberandindex)
        - [Parameters](#parameters-28)
        - [Returns](#returns-28)
        - [Example](#example-28)
      - [yue_getTransactionReceipt](#yue_gettransactionreceipt)
        - [Parameters](#parameters-29)
        - [Returns](#returns-29)
        - [Example](#example-29) 
      - [yue_newFilter](#yue_newfilter)
        - [A note on specifying topic filters:](#a-note-on-specifying-topic-filters)
        - [Parameters](#parameters-30)
        - [Returns](#returns-30)
        - [Example](#example-30)
      - [yue_newBlockFilter](#yue_newblockfilter)
        - [Parameters](#parameters-31)
        - [Returns](#returns-31)
        - [Example](#example-31)
      - [yue_newPendingTransactionFilter](#yue_newpendingtransactionfilter)
        - [Parameters](#parameters-32)
        - [Returns](#returns-32)
        - [Example](#example-32)
      - [yue_uninstallFilter](#yue_uninstallfilter)
        - [Parameters](#parameters-33)
        - [Returns](#returns-33)
        - [Example](#example-33)
      - [yue_getFilterChanges](#yue_getfilterchanges)
        - [Parameters](#parameters-34)
        - [Returns](#returns-34)
        - [Example](#example-34)
      - [yue_getFilterLogs](#yue_getfilterlogs)
        - [Parameters](#parameters-35)
        - [Returns](#returns-35)
        - [Example](#example-35)
      - [yue_getLogs](#yue_getlogs)
        - [Parameters](#parameters-36)
        - [Returns](#returns-36)
        - [Example](#example-36)
      - [yue_committeeNumber](#yue_committeeNumber)
        - [Parameters](#parameters-40)
        - [Returns](#returns-40)
        - [Example](#example-40)
      - [yue_getCommittee](#yue_getCommittee)
        - [Parameters](#parameters-44)
        - [Returns](#returns-44)
        - [Example](#example-44)
      - [yue_getRewardBlock](#yue_getRewardBlock)
        - [Parameters](#parameters-47)
        - [Returns](#returns-47)
        - [Example](#example-47)
      - [yue_getRecentChainRewardContent](#yue_getRecentChainRewardContent)
        - [Parameters](#parameters-52)
        - [Returns](#returns-52)
        - [Example](#example-52)        
      - [yue_getChainRewardContent](#yue_getChainRewardContent)
        - [Parameters](#parameters-53)
        - [Returns](#returns-53)
        - [Example](#example-53)        
      - [cpm_showGroup](#cpm_showGroup)
        - [Parameters](#parameters-54)
        - [Returns](#returns-54)
        - [Example](#example-54)
      - [cpm_listBasePermission](#cpm_listBasePermission)
        - [Parameters](#parameters-55)
        - [Returns](#returns-55)
        - [Example](#example-55)
      - [cpm_listPermission](#cpm_listPermission)
        - [Parameters](#parameters-56)
        - [Returns](#returns-56)
        - [Example](#example-56)
      - [cpm_showMyGroup](#cpm_showMyGroup)
        - [Parameters](#parameters-57)
        - [Returns](#returns-57)
        - [Example](#example-57)
      - [cpm_showBlackList](#cpm_showBlackList)
        - [Parameters](#parameters-58)
        - [Returns](#returns-58)
        - [Example](#example-58)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# JSON RPC API  

[JSON](http://json.org/) is a lightweight data-interchange format. It can represent numbers, strings, ordered sequences of values, and collections of name/value pairs.

[JSON-RPC](http://www.jsonrpc.org/specification) is a stateless, light-weight remote procedure call (RPC) protocol. Primarily this specification defines several data structures and the rules around their processing. It is transport agnostic in that the concepts can be used within the same process, over sockets, over HTTP, or in many various message passing environments. It uses JSON ([RFC 4627](http://www.ietf.org/rfc/rfc4627.txt)) as data format.

Taiyue  has experimental pub/sub support. See [this](https://github.com/truechain/truechain-engineering-code/wiki/RPC-PUB-SUB) page for more information.


## JavaScript API

To talk to an truechain node from inside a JavaScript application use the [web3.js](https://github.com/truechain/web3.js) library, which gives a convenient interface for the RPC methods.

## JSON-RPC Endpoint

Default JSON-RPC endpoints:
http://localhost:8545 


### Go

You can start the HTTP JSON-RPC with the `--rpc` flag
```bash
taiyue  --rpc
```

change the default port (8545) and listing address (localhost) with:

```bash
taiyue  --rpc --rpcaddr <ip> --rpcport <portnumber>
```

If accessing the RPC from a browser, CORS will need to be enabled with the appropriate domain set. Otherwise, JavaScript calls are limit by the same-origin policy and requests will fail:

```bash
taiyue  --rpc --rpccorsdomain "http://localhost:3000"
```

## JSON-RPC support
JSON-RPC 2.0/ Batch requests/  HTTP/  IPC/  WS

## The default block parameter

The following methods have an extra default block parameter:

- [yue_getBalance](#yue_getbalance)
- [yue_getCode](#yue_getcode)
- [yue_getTransactionCount](#yue_gettransactioncount)
- [yue_getStorageAt](#yue_getstorageat)
- [yue_call](#yue_call)
- [cpm_showGroup](#cpm_showGroup)
- [cpm_listBasePermission](#cpm_listBasePermission)
- [cpm_listPermission](#cpm_listPermission)
- [cpm_showMyGroup](#cpm_showMyGroup)
- [cpm_showBlackList](#cpm_showBlackList)

When requests are made that act on the state of truechain, the last default block parameter determines the height of the block.

The following options are possible for the defaultBlock parameter:

- `HEX String` - an integer block number
- `String "earliest"` for the earliest/genesis block
- `String "latest"` - for the latest mined block
- `String "pending"` - for the pending state/transactions

## Curl Examples Explained

The curl options below might return a response where the node complains about the content type, this is because the --data option sets the content type to application/x-www-form-urlencoded . If your node does complain, manually set the header by placing -H "Content-Type: application/json" at the start of the call.

The examples also do not include the URL/IP & port combination which must be the last argument given to curl e.x. 127.0.0.1:8545

## JSON-RPC methods

|   [yue](#yue)   |[cpm](#cpm) |[web3](#web3) |[net](#net) |
| :------------------:  |:-----------------:|:-----------------: |:-----------------: |
| [protocolVersion](#yue_protocolVersion)|[showGroup](#cpm_showGroup)|[clientVersion](#web3_clientVersion)|[version](#net_version)|
|[syncing](#yue_sycning)|[listBasePermission](#cpm_listBasePermission)|[sha3](#web3_sha3)| [peerCount](#net_peercount)|
|[coinbase](#yue_coinbase)|[listPermission](#cpm_listPermission)||[listening](#net_listening)|
|[gasPrice](#yue_gasPrice)|
|[accounts](#yue_accounts)|
|[blockNumber](#yue_blockNumber)  |
|[getBalance](#yue_getBalance)|
|[getStorageAt](#yue_getStorageAt)|
| [getTransactionCount](#yue_getTransactionCount)|
| [getBlockTransactionCountByHash](#yue_getBlockTransactionCountByHash)  | 
| [getBlockTransactionCountByNumber](#yue_getBlockTransactionCountByNumber)  |
|         [getCode](#yue_getCode)              |
|           [sign](#yue_sign)                   |
|     [sendTransaction](#yue_sendTransaction)            |
|    [sendRawTransaction](#yue_sendRawTransaction)      |
| [sendTrueRawTransaction](#yue_sendTrueRawTransaction)  |
|           [call](#yue_call)        |
|       [estimateGas](#yue_estimateGas)              |
| [getBlockByHash](#yue_getblockbyhash)        |
| [getBlockByNumber](#yue_getblockbynumber)         |
|[getTransactionByHash](#yue_gettransactionbyhash) |
|[getTransactionByBlockHashAndIndex](#yue_gettransactionbyblockhashandindex) |
|[getTransactionByBlockNumberAndIndex](#yue_gettransactionbyblocknumberandindex)|
|  [getTransactionReceipt](#yue_gettransactionreceipt)    |
|[newFilter](#yue_newfilter)|
|[newBlockFilter](#yue_newblockfilter)|
|[newPendingTransactionFilter](#yue_newpendingtransactionfilter)|
|[uninstallFilter](#yue_uninstallfilter)|
|[getFilterChanges](#yue_getfilterchanges)|
|[getFilterLogs](#yue_getfilterlogs)|
|[getLogs](#yue_getlogs)|
|     [committeeNumber](#yue_committeeNumber)      |
|       [getCommittee](#yue_getCommittee)       |
|      [getRewardBlock](#yue_getRewardBlock)    |



## JSON RPC API Reference

***

## web3

#### web3_clientVersion

Returns the current client version.

##### Parameters
none

##### Returns

`String` - The current client version.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":67}'

// Result
{
  "id":67,
  "jsonrpc":"2.0",
  "result": "Taiyue/v1.1.0-unstable-d4c05e98/linux-amd64/go1.10"
}
```

***

#### web3_sha3

Returns Keccak-256 (*not* the standardized SHA3-256) of the given data.

##### Parameters

1. `DATA` - the data to convert into a SHA3 hash.

##### Example Parameters
```js
params: [
  "0x68656c6c6f20776f726c64"
]
```

##### Returns

`DATA` - The SHA3 result of the given string.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"web3_sha3","params":["0x68656c6c6f20776f726c64"],"id":64}'

// Result
{
  "id":64,
  "jsonrpc": "2.0",
  "result": "0x47173285a8d7341e5e972fc677286384f802f8ef42a5ec5f03bbfa254cb01fad"
}
```

***

## net

#### net_version

Returns the current network id.

##### Parameters
none

##### Returns

`String` - The current network id.
- `"19330"`: Truechain Mainnet
- `"18928"`: Testnet
- `"100"`:   Devnet

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"net_version","params":[],"id":67}'

// Result
{
  "id":67,
  "jsonrpc": "2.0",
  "result": "19330"
}
```

***

#### net_listening

Returns `true` if client is actively listening for network connections.

##### Parameters
none

##### Returns

`Boolean` - `true` when listening, otherwise `false`.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"net_listening","params":[],"id":67}'

// Result
{
  "id":67,
  "jsonrpc":"2.0",
  "result":true
}
```

***

#### net_peerCount

Returns number of peers currently connected to the client.

##### Parameters
none

##### Returns

`QUANTITY` - integer of the number of connected peers.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":74}'

// Result
{
  "id":74,
  "jsonrpc": "2.0",
  "result": "0x2" // 2
}
```

***
## Etrue

#### yue_protocolVersion

Returns the current truechain protocol version.

##### Parameters
none

##### Returns

`String` - The current truechain protocol version.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_protocolVersion","params":[],"id":67}'

// Result
{
  "id":67,
  "jsonrpc": "2.0",
  "result": "0x40"
}
```

***

#### yue_syncing

Returns an object with data about the sync status or `false`.


##### Parameters
none

##### Returns

`Object|Boolean`, An object with sync status data or `FALSE`, when not syncing:
  - `currentFastBlock`: `QUANTITY` -current block number(fastchain)
  - `highestFastBlock`: `QUANTITY` - already highest block number(fastchain)
  - `knownStates`:  `String` -already know state 
  - `pulledStates`: `String` -already complete state
  - `startingFastBlock`: `QUANTITY` -start sync block number(fastchain)

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_syncing","params":[],"id":1}'

// Result
{
	"jsonrpc": "2.0",
	"id": 1,
	"result": {
		"currentFastBlock": "0x2e9a",
		"highestFastBlock": "0x3a3d2",
		"knownStates": "0x0",
		"pulledStates": "0x0",
	}
}
// Or when not syncing
{
  "id":1,
  "jsonrpc": "2.0",
  "result": false
}
```

***

#### yue_coinbase

Returns the client coinbase address.


##### Parameters
none

##### Returns

`DATA`, 20 bytes - the current coinbase address.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_coinbase","params":[],"id":64}'

// Result
{
  "id":64,
  "jsonrpc": "2.0",
  "result": "0xc94770007dda54cF92009BFF0dE90c06F603a09f"
}
```

***

#### yue_mining

Returns `true` if client is actively mining new blocks.

##### Parameters
none

##### Returns

`Boolean` - returns `true` of the client is mining, otherwise `false`.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_mining","params":[],"id":71}'

// Result
{
  "id":71,
  "jsonrpc": "2.0",
  "result": true
}

```

***

#### yue_hashrate

Returns the number of hashes per second that the node is mining with.

##### Parameters
none

##### Returns

`QUANTITY` - number of hashes per second.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_hashrate","params":[],"id":71}'

// Result
{
  "id":71,
  "jsonrpc": "2.0",
  "result": "0x38a"
}

```

***

#### yue_gasPrice

Returns the current price per gas in wei.

##### Parameters
none

##### Returns

`QUANTITY` - integer of the current gas price in wei.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_gasPrice","params":[],"id":73}'

// Result
{
  "id":73,
  "jsonrpc": "2.0",
  "result": "0xf4240" // 1000000
}
```

***

#### yue_accounts

Returns a list of addresses owned by client.


##### Parameters
none

##### Returns

`Array of DATA`, 20 Bytes - addresses owned by the client.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_accounts","params":[],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": ["0xc94770007dda54cF92009BFF0dE90c06F603a09f"]
}
```

***

#### yue_blockNumber

Returns the number of most recent block.

##### Parameters
none

##### Returns

`QUANTITY` - integer of the current block number the client is on.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_blockNumber","params":[],"id":1}'

// Result
{
  "id":83,
  "jsonrpc": "2.0",
  "result": "0xc94" // 1207
}
```

***

#### yue_getBalance

Returns the balance of the account of given address.

##### Parameters

1. `DATA`, 20 Bytes - address to check for balance.
2. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)

##### Example Parameters
```js
params: [
   '0xc94770007dda54cF92009BFF0dE90c06F603a09f',
   'latest'
]
```

##### Returns

`QUANTITY` - integer of the current balance in wei.


##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getBalance","params":["0xc94770007dda54cF92009BFF0dE90c06F603a09f", "latest"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x0234c8a3397aab58" // 158972490234375000
}
```

***

#### yue_getStorageAt

Returns the value from a storage position at a given address. 

##### Parameters

1. `DATA`, 20 Bytes - address of the storage.
2. `QUANTITY` - integer of the position in the storage.
3. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)

##### Returns

`DATA` - the value at this storage position.

##### Example
Calculating the correct position depends on the storage to retrieve. Consider the following contract deployed at `0x295a70b2de5e3953354a6a8344e616ed314d7251` by address `0x391694e7e0b0cce554cb130d723a9d27458f9298`.

```
contract Storage {
    uint pos0;
    mapping(address => uint) pos1;
    
    function Storage() {
        pos0 = 1234;
        pos1[msg.sender] = 5678;
    }
}
```

Retrieving the value of pos0 is straight forward:

```js
curl -X POST --data '{"jsonrpc":"2.0", "method": "yue_getStorageAt", "params": ["0x295a70b2de5e3953354a6a8344e616ed314d7251", "0x0", "latest"], "id": 1}' localhost:8545

{"jsonrpc":"2.0","id":1,"result":"0x00000000000000000000000000000000000000000000000000000000000004d2"}
```

Retrieving an element of the map is harder. The position of an element in the map is calculated with:
```js
keccack(LeftPad32(key, 0), LeftPad32(map position, 0))
```

This means to retrieve the storage on pos1["0x391694e7e0b0cce554cb130d723a9d27458f9298"] we need to calculate the position with:
```js
keccak(decodeHex("000000000000000000000000391694e7e0b0cce554cb130d723a9d27458f9298" + "0000000000000000000000000000000000000000000000000000000000000001"))
```
The taiyue  console which comes with the web3 library can be used to make the calculation:
```js
> var key = "000000000000000000000000391694e7e0b0cce554cb130d723a9d27458f9298" + "0000000000000000000000000000000000000000000000000000000000000001"
undefined
> web3.sha3(key, {"encoding": "hex"})
"0x6661e9d6d8b923d5bbaab1b96e1dd51ff6ea2a93520fdc9eb75d059238b8c5e9"
```
Now to fetch the storage:
```js
curl -X POST --data '{"jsonrpc":"2.0", "method": "yue_getStorageAt", "params": ["0x295a70b2de5e3953354a6a8344e616ed314d7251", "0x6661e9d6d8b923d5bbaab1b96e1dd51ff6ea2a93520fdc9eb75d059238b8c5e9", "latest"], "id": 1}' localhost:8545

{"jsonrpc":"2.0","id":1,"result":"0x000000000000000000000000000000000000000000000000000000000000162e"}

```

***

#### yue_getTransactionCount

Returns the number of transactions *sent* from an address.


##### Parameters

1. `DATA`, 20 Bytes - address.
2. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)

##### Example Parameters
```js
params: [
   '0xc94770007dda54cF92009BFF0dE90c06F603a09f',
   'latest' // state at the latest block
]
```

##### Returns

`QUANTITY` - integer of the number of transactions send from this address.


##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getTransactionCount","params":["0xc94770007dda54cF92009BFF0dE90c06F603a09f","latest"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x1" // 1
}
```

***

#### yue_getBlockTransactionCountByHash

Returns the number of transactions in a block from a block matching the given block hash.


##### Parameters

1. `DATA`, 32 Bytes - hash of a block.

##### Example Parameters
```js
params: [
   '0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238'
]
```

##### Returns

`QUANTITY` - integer of the number of transactions in this block.


##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getBlockTransactionCountByHash","params":["0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xc" // 11
}
```

***

#### yue_getBlockTransactionCountByNumber
> > 
Returns the number of transactions in a block matching the given block number.


##### Parameters

1. `QUANTITY|TAG` - integer of a block number, or the string `"earliest"`, `"latest"` or `"pending"`, as in the [default block parameter](#the-default-block-parameter).

##### Example Parameters
```js
params: [
   '0xe8', // 232
]
```

##### Returns

`QUANTITY` - integer of the number of transactions in this block.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getBlockTransactionCountByNumber","params":["0xe8"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xa" // 10
}
```

***

#### yue_getCode

Returns code at a given address.


##### Parameters

1. `DATA`, 20 Bytes - address.
2. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter).

##### Example Parameters
```js
params: [
   '0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b',
   '0x2'  // 2
]
```

##### Returns

`DATA` - the code from the given address.


##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getCode","params":["0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b", "0x2"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x600160008035811a818181146012578301005b601b6001356025565b8060005260206000f25b600060078202905091905056"
}
```

***

#### yue_sign

The sign method calculates an Truechain specific signature with: `sign(keccak256("\x19Truechain Signed Message:\n" + len(message) + message)))`.

By adding a prefix to the message makes the calculated signature recognisable as an Truechain specific signature. This prevents misuse where a malicious DApp can sign arbitrary data (e.g. transaction) and use the signature to impersonate the victim.

**Note** the address to sign with must be unlocked. 

##### Parameters
account, message

1. `DATA`, 20 Bytes - address.
2. `DATA`, N Bytes - message to sign.

##### Returns

`DATA`: Signature

##### Example

```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_sign","params":["0x9b2055d370f73ec7d8a03e965129118dc8f5bf83", "0xdeadbeaf"],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xa3f20717a250c2b0b729b7e5becbff67fdaef7e0699da4de7ca5895b02a170a12d887fd3b17bfdce3481f10bea41f45ba9f709d39ce8325427b57afcfc994cee1b"
}
```

An example how to use solidity ecrecover to verify the signature calculated with `yue_sign` can be found [here](https://gist.github.com/bas-vk/d46d83da2b2b4721efb0907aecdb7ebd). The contract is deployed on the testnet Ropsten and Rinkeby.

***

#### yue_sendTransaction

Creates new message call transaction or a contract creation, if the data field contains code.

##### Parameters

1. `Object` - The transaction object
  - `from`: `DATA`, 20 Bytes - The address the transaction is send from.
  - `to`: `DATA`, 20 Bytes - (optional when creating new contract) The address the transaction is directed to.
  - `gas`: `QUANTITY`  - (optional, default: 90000) Integer of the gas provided for the transaction execution. It will return unused gas.
  - `gasPrice`: `QUANTITY`  - (optional, default: To-Be-Determined) Integer of the gasPrice used for each paid gas
  - `value`: `QUANTITY`  - (optional) Integer of the value sent with this transaction
  - `data`: `DATA`  - The compiled code of a contract OR the hash of the invoked method signature and encoded parameters. 
  - `nonce`: `QUANTITY`  - (optional) Integer of a nonce. This allows to overwrite your own pending transactions that use the same nonce.

##### Example Parameters
```js
params: [{
  "from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155",
  "to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
  "gas": "0x76c0", // 30400
  "gasPrice": "0x9184e72a000", // 10000000000000
  "value": "0x9184e72a", // 2441406250
  "data": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"
}]
```

##### Returns

`DATA`, 32 Bytes - the transaction hash, or the zero hash if the transaction is not yet available.

Use [yue_getTransactionReceipt](#yue_gettransactionreceipt) to get the contract address, after the transaction was mined, when you created a contract.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_sendTransaction","params":[{see above}],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331"
}
```

***

#### yue_sendRawTransaction

Creates new message call transaction or a contract creation for signed transactions.

##### Parameters

1. `DATA`, The signed transaction data.

##### Example Parameters
```js
params: ["0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"]
```

##### Returns

`DATA`, 32 Bytes - the transaction hash, or the zero hash if the transaction is not yet available.

Use [yue_getTransactionReceipt](#yue_gettransactionreceipt) to get the contract address, after the transaction was mined, when you created a contract.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_sendRawTransaction","params":[{see above}],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331"
}
```

***

#### yue_sendTrueRawTransaction

When transaction contain payer or fee,Creates new message call transaction or a contract creation for signed transactions.

##### Parameters

1. `DATA`, The signed transaction data.

##### Example Parameters
```js
params: ["0xf8c60183989680834c4b4094bea78fea68dba84363d0f9b79219ddf5991ccb2a880de0b6b3a76400008094cfb7ec3ac64a3afde043a5b32212d0b9c25b5d808081eba07cc4b8300a8ab6a7d6aee713f6dc61311848bf827794c370873ca334e7cc2cc1a05cd365ffc46cada820911e3c11123e36245ed1cec7943038632715a89a421b0281eca037d6e60016bd70371fd45a2fadd63f8824b34331f2cb5f7fe69f04df7f6d9caea04e05dda8cffa3e453aa474f955eef97fe63e9c9721860aaea379a0ace111fd16"]
```

##### Returns

`DATA`, 32 Bytes - the transaction hash, or the zero hash if the transaction is not yet available.

Use [yue_getTransactionReceipt](#yue_gettransactionreceipt) to get the contract address, after the transaction was mined, when you created a contract.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_sendTrueRawTransaction","params":[{see above}],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xc7509ef7672e1c1d59cec2854d3d074d442984382bd03c665c2e82ebfdacc25e"
}
```

***

#### yue_call

Executes a new message call immediately without creating a transaction on the block chain.


##### Parameters

1. `Object` - The transaction call object
  - `from`: `DATA`, 20 Bytes - (optional) The address the transaction is sent from.
  - `to`: `DATA`, 20 Bytes  - The address the transaction is directed to.
  - `gas`: `QUANTITY`  - (optional) Integer of the gas provided for the transaction execution. yue_call consumes zero gas, but this parameter may be needed by some executions.
  - `gasPrice`: `QUANTITY`  - (optional) Integer of the gasPrice used for each paid gas
  - `value`: `QUANTITY`  - (optional) Integer of the value sent with this transaction
  - `data`: `DATA`  - (optional) Hash of the method signature and encoded parameters
2. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)

##### Returns

`DATA` - the return value of executed contract.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_call","params":[{see yue_sendTransaction parameter}],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x"
}
```

***

#### yue_estimateGas

Generates and returns an estimate of how much gas is necessary to allow the transaction to complete. The transaction will not be added to the blockchain. Note that the estimate may be significantly more than the amount of gas actually used by the transaction, for a variety of reasons including EVM mechanics and node performance.

##### Parameters

See [yue_call](#yue_call) parameters, expect that all properties are optional. If no gas limit is specified taiyue  uses the block gas limit from the pending block as an upper bound. As a result the returned estimate might not be enough to executed the call/transaction when the amount of gas is higher than the pending block gas limit.

##### Returns

`QUANTITY` - the amount of gas used.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_estimateGas","params":[{see yue_sendTransaction parameter}],"id":1}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x5208" // 21000
}
```

***

#### yue_getBlockByHash

Returns information about a block by hash.


##### Parameters

1. `DATA`, 32 Bytes - Hash of a block.
2. `Boolean` - If `true` it returns the full transaction objects, if `false` only the hashes of the transactions.

##### Example Parameters
```js
params: [
   '0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331',
   true
]
```

##### Returns

`Object` - A block object, or `null` when no block was found:

  - `committeeRoot`: `DATA`, 32 Bytes - hash of the committtee.
  - `extraData`: `DATA` - the "extra data" field of this block.
  - `gasLimit`: `QUANTITY` - the maximum gas allowed in this block.
  - `gasUsed`: `QUANTITY` - the total used gas by all transactions in this block.
  - `hash`: `DATA`, 32 Bytes - hash of the block. `null` when its pending block.
  - `logsBloom`: `DATA`, 256 Bytes - the bloom filter for the logs of the block. `null` when its pending block.
  - `maker`: `DATA`, 20 Bytes - the address of the beneficiary to whom the mining rewards were given.
  - `number`: `QUANTITY` - the block number. `null` when its pending block.
  - `parentHash`: `DATA`, 32 Bytes - hash of the parent block.
  - `receiptsRoot`: `DATA`, 32 Bytes - the root of the receipts trie of the block.
  - `signs`: `Array`, committee signs.
      - `fastHash`: `DATA`, 32 Bytes - hash of the fast block.
      - `fastHeight`: `QUANTITY`- the fast block number.
      - `result`: `QUANTITY`- the vote.
      - `sign`: `DATA`, 32 Bytes - committee sign hash.
  - `size`: `QUANTITY` - integer the size of this block in bytes.
  - `stateRoot`: `DATA`, 32 Bytes - the root of the final state trie of the block.
  - `switchInfos`: `Array`, committee member switch.
  - `timestamp`: `QUANTITY` - the unix timestamp for when the block was collated.
  - `transactions`: `Array` - Array of transaction objects, or 32 Bytes transaction hashes depending on the last given parameter.
  - `transactionsRoot`: `DATA`, 32 Bytes - the root of the transaction trie of the block.


##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getBlockByHash","params":["0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d15273312", true],"id":1}'

// Result
{
"id":1,
"jsonrpc":"2.0",
"result": {
    {
"committeeRoot":"0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
"extraData":"0x",
"gasLimit":"0xb71b00","gasUsed":"0x0",
"hash":"0xd58570f394347e6b73c4beeabfb75f8b4a6c6f08c71f159a233309365836e3d2",
"logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
"maker":"0x49fc88c2576b4f015cf75dae80e87a815d832888",
"number":"0xab4",
"parentHash":"0x0832d972f5b16ddefc3de154cc0a5a4ea16be2991be19bd740ae3486a83ff59f",
"receiptsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
"signs":[{"fastHash":"0xd58570f394347e6b73c4beeabfb75f8b4a6c6f08c71f159a233309365836e3d2",
"fastHeight":"0xab4","result":1,
"sign":"0x7a07be32cce585b6d74e6134022c973b6433dcb87447ec456712f5d3b40b8907403ea24c81309aa090e7469fc761372de2e2d32beddf0031eed1aa557185cbc101"},
{"fastHash":"0xd58570f394347e6b73c4beeabfb75f8b4a6c6f08c71f159a233309365836e3d2","fastHeight":"0xab4","result":1,"sign":"0x4f1033692e2f354409002ff0ce9eb20d4edb676f6c02dc58223c9d2d15eebcaf4071c2efc630a44d78865da714ae694cd690d4b0d02b393d64ca377c63594a6e01"},{"fastHash":"0xd58570f394347e6b73c4beeabfb75f8b4a6c6f08c71f159a233309365836e3d2","fastHeight":"0xab4","result":1,"sign":"0xc8303a5c76fb70e834b63e70180af9720ac09eda59327a0e6be3ab85fcfcbb9b40434ae7dcd23df13fe6a55c1967d29de7db5c5e545674b6849a1a4eabb59b4b00"},
{"fastHash":"0xd58570f394347e6b73c4beeabfb75f8b4a6c6f08c71f159a233309365836e3d2","fastHeight":"0xab4","result":1,"sign":"0x041df0a05407cb302695babfeff03d669d300e76cc2d33305512dc0859aeb4dc47b68065b5d62bd88a6b60e3993ed07ae0a64223681084c5c958cdd2041f42a100"},
{"fastHash":"0xd58570f394347e6b73c4beeabfb75f8b4a6c6f08c71f159a233309365836e3d2","fastHeight":"0xab4","result":1,"sign":"0x8b8c97a4155c2b687b0eb90e1a716ede85c1b32ec7b164c0fa721f1b18ada4c41bc46373419d625ef8f0368b123bf86a60b07c168ebb5b97de4b9095847fad5001"}],"size":"0x40a","stateRoot":"0x5c7127948504801c7db0ef17df87950b471a94d6f5332d39ceff41298f3f6b74",
"switchInfos":[],"timestamp":"0x5ce25206","transactions":[],
"transactionsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421"}
  }
}
```

***

#### yue_getBlockByNumber

Returns information about a block by block number.

##### Parameters

1. `QUANTITY|TAG` - integer of a block number, or the string `"earliest"`, `"latest"` or `"pending"`, as in the [default block parameter](#the-default-block-parameter).
2. `Boolean` - If `true` it returns the full transaction objects, if `false` only the hashes of the transactions.

##### Example Parameters
```js
params: [
   '0x1b4', // 436
   true
]
```

##### Returns

See [yue_getBlockByHash](#yue_getblockbyhash)

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getBlockByNumber","params":["0x1b4", true],"id":1}'
```

Result see [yue_getBlockByHash](#yue_getblockbyhash)

***

#### yue_getTransactionByHash

Returns the information about a transaction requested by transaction hash.


##### Parameters

1. `DATA`, 32 Bytes - hash of a transaction

##### Example Parameters
```js
params: [
   "0x88df016429689c079f3b2f6ad39fa052532c56795b733da78a91ebe6a713944b"
]
```

##### Returns

`Object` - A transaction object, or `null` when no transaction was found:

  - `blockHash`: `DATA`, 32 Bytes - hash of the block where this transaction was in. `null` when its pending.
  - `blockNumber`: `QUANTITY` - block number where this transaction was in. `null` when its pending.
  - `from`: `DATA`, 20 Bytes - address of the sender.
  - `gas`: `QUANTITY` - gas provided by the sender.
  - `gasPrice`: `QUANTITY` - gas price provided by the sender in Wei.
  - `hash`: `DATA`, 32 Bytes - hash of the transaction.
  - `input`: `DATA` - the data send along with the transaction.
  - `nonce`: `QUANTITY` - the number of transactions made by the sender prior to this one.
  - `to`: `DATA`, 20 Bytes - address of the receiver. `null` when its a contract creation transaction.
  - `transactionIndex`: `QUANTITY` - integer of the transaction's index position in the block. `null` when its pending.
  - `value`: `QUANTITY` - value transferred in Wei.
  - `v`: `QUANTITY` - ECDSA recovery id
  - `r`: `DATA`, 32 Bytes - ECDSA signature r
  - `s`: `DATA`, 32 Bytes - ECDSA signature s

  - `payer`: `DATA`, 20 Bytes - address of the payer.
  - `fee`: `QUANTITY` - transaction fee in Wei.
  - `pv`: `QUANTITY` - ECDSA recovery id
  - `pr`: `DATA`, 32 Bytes - ECDSA signature pr
  - `ps`: `DATA`, 32 Bytes - ECDSA signature ps


##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getTransactionByHash","params":["0x88df016429689c079f3b2f6ad39fa052532c56795b733da78a91ebe6a713944b"],"id":1}'

// Result
{
  "jsonrpc":"2.0",
  "id":1,
  "result":{
    "blockHash":"0x1d59ff54b1eb26b013ce3cb5fc9dab3705b415a67127a003c3e61eb445bb8df2",
    "blockNumber":"0x5daf3b", // 6139707
    "from":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",
    "gas":"0xc350", // 50000
    "gasPrice":"0x4a817c800", // 20000000000
    "hash":"0x88df016429689c079f3b2f6ad39fa052532c56795b733da78a91ebe6a713944b",
    "input":"0x68656c6c6f21",
    "nonce":"0x15", // 21
    "to":"0xf02c1c8e6114b1dbe8937a39260b5b0a374432bb",
    "transactionIndex":"0x41", // 65
    "value":"0xf3dbb76162000", // 4290000000000000
    "v":"0x25", // 37
    "r":"0x1b5e176d927f8e9ab405058b2d2457392da3e20f328b16ddabcebc33eaac5fea",
    "s":"0x4ba69724e8f69de52f0125ad8b3c5c2cef33019bac3249e2c0a2192766d1721c"
    "payer":null,
    "fee":null,
    "pv":null,
    "pr":null,
    "ps":null
  }
}
```

***

#### yue_getTransactionByBlockHashAndIndex

Returns information about a transaction by block hash and transaction index position.


##### Parameters

1. `DATA`, 32 Bytes - hash of a block.
2. `QUANTITY` - integer of the transaction index position.

##### Example Parameters
```js
params: [
   '0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331',
   '0x0' // 0
]
```

##### Returns

See [yue_getTransactionByHash](#yue_gettransactionbyhash)

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getTransactionByBlockHashAndIndex","params":["0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b", "0x0"],"id":1}'
```

Result see [yue_getTransactionByHash](#yue_gettransactionbyhash)

***

#### yue_getTransactionByBlockNumberAndIndex

Returns information about a transaction by block number and transaction index position.


##### Parameters

1. `QUANTITY|TAG` - a block number, or the string `"earliest"`, `"latest"` or `"pending"`, as in the [default block parameter](#the-default-block-parameter).
2. `QUANTITY` - the transaction index position.

##### Example Parameters
```js
params: [
   '0x29c', // 668
   '0x0' // 0
]
```

##### Returns

See [yue_getTransactionByHash](#yue_gettransactionbyhash)

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getTransactionByBlockNumberAndIndex","params":["0x29c", "0x0"],"id":1}'
```

Result see [yue_getTransactionByHash](#yue_gettransactionbyhash)

***

#### yue_getTransactionReceipt

Returns the receipt of a transaction by transaction hash.

**Note** That the receipt is not available for pending transactions.


##### Parameters

1. `DATA`, 32 Bytes - hash of a transaction

##### Example Parameters
```js
params: [
   '0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238'
]
```

##### Returns

`Object` - A transaction receipt object, or `null` when no receipt was found:

  - `transactionHash `: `DATA`, 32 Bytes - hash of the transaction.
  - `transactionIndex`: `QUANTITY` - integer of the transaction's index position in the block.
  - `blockHash`: `DATA`, 32 Bytes - hash of the block where this transaction was in.
  - `blockNumber`: `QUANTITY` - block number where this transaction was in.
  - `from`: `DATA`, 20 Bytes - address of the sender.
  - `to`: `DATA`, 20 Bytes - address of the receiver. null when it's a contract creation transaction.
  - `cumulativeGasUsed `: `QUANTITY ` - The total amount of gas used when this transaction was executed in the block.
  - `gasUsed `: `QUANTITY ` - The amount of gas used by this specific transaction alone.
  - `contractAddress `: `DATA`, 20 Bytes - The contract address created, if the transaction was a contract creation, otherwise `null`.
  - `to`: `DATA`, 20 Bytes  - The address the transaction is directed to.
  - `logs`: `Array` - Array of log objects, which this transaction generated.
  - `logsBloom`: `DATA`, 256 Bytes - Bloom filter for light clients to quickly retrieve related logs.
  
It also returns _either_ :

  - `root` : `DATA` 32 bytes of post-transaction stateroot (pre Byzantium)
  - `status`: `QUANTITY` either `1` (success) or `0` (failure) 


##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getTransactionReceipt","params":["0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"],"id":1}'

// Result
{
"id":1,
"jsonrpc":"2.0",
"result": {
     transactionHash: '0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238',
     transactionIndex:  '0x1', // 1
     blockNumber: '0xb', // 11
     blockHash: '0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b',
     cumulativeGasUsed: '0x33bc', // 13244
     gasUsed: '0x4dc', // 1244
     contractAddress: '0xb60e8dd61c5d32be8058bb8eb970870f07233155', // or null, if none was created
     logs: [{
         // logs as returned by getFilterLogs, etc.
     }, ...],
     logsBloom: "0x00...0", // 256 byte bloom filter
     status: '0x1'
  }
}
```

***

#### yue_newFilter

Creates a filter object, based on filter options, to notify when the state changes (logs).
To check if the state has changed, call [yue_getFilterChanges](#yue_getfilterchanges).

##### A note on specifying topic filters:
Topics are order-dependent. A transaction with a log with topics [A, B] will be matched by the following topic filters:
* `[]` "anything"
* `[A]` "A in first position (and anything after)"
* `[null, B]` "anything in first position AND B in second position (and anything after)"
* `[A, B]` "A in first position AND B in second position (and anything after)"
* `[[A, B], [A, B]]` "(A OR B) in first position AND (A OR B) in second position (and anything after)"

##### Parameters

1. `Object` - The filter options:
  - `fromBlock`: `QUANTITY|TAG` - (optional, default: `"latest"`) Integer block number, or `"latest"` for the last mined block or `"pending"`, `"earliest"` for not yet mined transactions.
  - `toBlock`: `QUANTITY|TAG` - (optional, default: `"latest"`) Integer block number, or `"latest"` for the last mined block or `"pending"`, `"earliest"` for not yet mined transactions.
  - `address`: `DATA|Array`, 20 Bytes - (optional) Contract address or a list of addresses from which logs should originate.
  - `topics`: `Array of DATA`,  - (optional) Array of 32 Bytes `DATA` topics. Topics are order-dependent. Each topic can also be an array of DATA with "or" options.

##### Example Parameters
```js
params: [{
  "fromBlock": "0x1",
  "toBlock": "0x2",
  "address": "0x8888f1f195afa192cfee860698584c030f4c9db1",
  "topics": ["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b", null, ["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b", "0x0000000000000000000000000aff3454fce5edbc8cca8697c15331677e6ebccc"]]
}]
```

##### Returns

`QUANTITY` - A filter id.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_newFilter","params":[{"topics":["0x0000000000000000000000000000000000000000000000000000000012341234"]}],"id":73}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x1" // 1
}
```

***

#### yue_newBlockFilter

Creates a filter in the node, to notify when a new block arrives.
To check if the state has changed, call [yue_getFilterChanges](#yue_getfilterchanges).

##### Parameters
None

##### Returns

`QUANTITY` - A filter id.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_newBlockFilter","params":[],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":  "2.0",
  "result": "0x1" // 1
}
```

***

#### yue_newPendingTransactionFilter

Creates a filter in the node, to notify when new pending transactions arrive.
To check if the state has changed, call [yue_getFilterChanges](#yue_getfilterchanges).

##### Parameters
None

##### Returns

`QUANTITY` - A filter id.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_newPendingTransactionFilter","params":[],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":  "2.0",
  "result": "0x1" // 1
}
```

***

#### yue_uninstallFilter

Uninstalls a filter with given id. Should always be called when watch is no longer needed.
Additonally Filters timeout when they aren't requested with [yue_getFilterChanges](#yue_getfilterchanges) for a period of time.


##### Parameters

1. `QUANTITY` - The filter id.

##### Example Parameters
```js
params: [
  "0xb" // 11
]
```

##### Returns

`Boolean` - `true` if the filter was successfully uninstalled, otherwise `false`.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_uninstallFilter","params":["0xb"],"id":73}'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": true
}
```

***

#### yue_getFilterChanges

Polling method for a filter, which returns an array of logs which occurred since last poll.


##### Parameters

1. `QUANTITY` - the filter id.

##### Example Parameters
```js
params: [
  "0x16" // 22
]
```

##### Returns

`Array` - Array of log objects, or an empty array if nothing has changed since last poll.

- For filters created with `yue_newBlockFilter` the return are block hashes (`DATA`, 32 Bytes), e.g. `["0x3454645634534..."]`.
- For filters created with `yue_newPendingTransactionFilter ` the return are transaction hashes (`DATA`, 32 Bytes), e.g. `["0x6345343454645..."]`.
- For filters created with `yue_newFilter` logs are objects with following params:

  - `removed`: `TAG` - `true` when the log was removed, due to a chain reorganization. `false` if its a valid log.
  - `logIndex`: `QUANTITY` - integer of the log index position in the block. `null` when its pending log.
  - `transactionIndex`: `QUANTITY` - integer of the transactions index position log was created from. `null` when its pending log.
  - `transactionHash`: `DATA`, 32 Bytes - hash of the transactions this log was created from. `null` when its pending log.
  - `blockHash`: `DATA`, 32 Bytes - hash of the block where this log was in. `null` when its pending. `null` when its pending log.
  - `blockNumber`: `QUANTITY` - the block number where this log was in. `null` when its pending. `null` when its pending log.
  - `address`: `DATA`, 20 Bytes - address from which this log originated.
  - `data`: `DATA` - contains the non-indexed arguments of the log.
  - `topics`: `Array of DATA` - Array of 0 to 4 32 Bytes `DATA` of indexed log arguments. (In *solidity*: The first topic is the *hash* of the signature of the event (e.g. `Deposit(address,bytes32,uint256)`), except you declared the event with the `anonymous` specifier.)

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getFilterChanges","params":["0x16"],"id":73}'

// Result
{
  "id":1,
  "jsonrpc":"2.0",
  "result": [{
    "logIndex": "0x1", // 1
    "blockNumber":"0x1b4", // 436
    "blockHash": "0x8216c5785ac562ff41e2dcfdf5785ac562ff41e2dcfdf829c5a142f1fccd7d",
    "transactionHash":  "0xdf829c5a142f1fccd7d8216c5785ac562ff41e2dcfdf5785ac562ff41e2dcf",
    "transactionIndex": "0x0", // 0
    "address": "0x16c5785ac562ff41e2dcfdf829c5a142f1fccd7d",
    "data":"0x0000000000000000000000000000000000000000000000000000000000000000",
    "topics": ["0x59ebeb90bc63057b6515673c3ecf9438e5058bca0f92585014eced636878c9a5"]
    },{
      ...
    }]
}
```

***

#### yue_getFilterLogs

Returns an array of all logs matching filter with given id.


##### Parameters

1. `QUANTITY` - The filter id.

##### Example Parameters
```js
params: [
  "0x16" // 22
]
```

##### Returns

See [yue_getFilterChanges](#yue_getfilterchanges)

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getFilterLogs","params":["0x16"],"id":74}'
```

Result see [yue_getFilterChanges](#yue_getfilterchanges)

***

#### yue_getLogs

Returns an array of all logs matching a given filter object.

##### Parameters

1. `Object` - The filter options:
  - `fromBlock`: `QUANTITY|TAG` - (optional, default: `"latest"`) Integer block number, or `"latest"` for the last mined block or `"pending"`, `"earliest"` for not yet mined transactions.
  - `toBlock`: `QUANTITY|TAG` - (optional, default: `"latest"`) Integer block number, or `"latest"` for the last mined block or `"pending"`, `"earliest"` for not yet mined transactions.
  - `address`: `DATA|Array`, 20 Bytes - (optional) Contract address or a list of addresses from which logs should originate.
  - `topics`: `Array of DATA`,  - (optional) Array of 32 Bytes `DATA` topics. Topics are order-dependent. Each topic can also be an array of DATA with "or" options.
  - `blockhash`:  `DATA`, 32 Bytes - (optional) With the addition of EIP-234 (Taiyue >= v1.8.13 or Parity >= v2.1.0), `blockHash` is a new filter option which restricts the logs returned to the single block with the 32-byte hash `blockHash`.  Using `blockHash` is equivalent to `fromBlock` = `toBlock` = the block number with hash `blockHash`.  If `blockHash` is present in the filter criteria, then neither `fromBlock` nor `toBlock` are allowed.

##### Example Parameters
```js
params: [{
  "topics": ["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b"]
}]
```

##### Returns

See [yue_getFilterChanges](#yue_getfilterchanges)

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"yue_getLogs","params":[{"topics":["0x000000000000000000000000a94f5374fce5edbc8e2a8697c15331677e6ebf0b"]}],"id":74}'
```

Result see [yue_getFilterChanges](#yue_getfilterchanges)

***

#### yue_committeeNumber

get current committee number


##### Parameters
none


##### Returns

QUANTITY - integer of the current committee number.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0", "method":"yue_committeeNumber", "params":[],"id":100}'

// Result
{
   "jsonrpc": "2.0",
   "id": 100,
   "result": 8
}
```

***
#### yue_getCommittee

get committee member infomation


##### Parameters
  ```js
params: ["0x1"]
```


##### Returns

- `backups`: `Array` - Array of backup committee members, each committee member info contains pubkey、 coinbase、flag、type.
- `beginNumber`: `QUANTITY` - the begin fast block number.
- `endNumber`: `QUANTITY` - the end fast block number.
- `id`: `QUANTITY` - committeeId.
- `memberCount`: `QUANTITY` - the number of committee members .
- `members`: `Array` - Array of  committee members.


##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0", "method":"yue_getCommittee", "params":["0x1"],"id":100}'

// Result
{
	"jsonrpc": "2.0",
	"id": 100,
	"result": {
                beginNumber: 3000,
                endNumber: 3999,
                id: 3,
                memberCount: 4,
                members: [{
                    PKey: "04bdf9699d20b4ebabe76e76260480e5492c87aaeda51b138bd22c6d66b69549313dc3eb8c96dc9a1cbbf3b347322c51c05afdd609622277444e0f07e6bd35d8bd",
                    coinbase: "0x68231c69431cd7592356abac59e7a9d325406653",
                    flag: 161,
                    type: 162
                }, {
                    PKey: "045e1711b6cd8550a5e5466f7f0868b5507929cb69c2f0fca84f8f94816eb40a808ea8a77c3d83c9d16341acb037fbea2f7d9d4af46326defa39b408f40f28fb98",
                    coinbase: "0xf7547ab248cedcd8ddee37b3e2e331061898f869",
                    flag: 161,
                    type: 162
                }, {
                    PKey: "041b931d350257e881f27bce2563d98c99b13ca4f525a0662f5e7d53f085edff0dca8ceaae550c9f4ceecf217f72806a48a48fb024916392ae41d7c45168e89b94",
                    coinbase: "0xa9b892d0a141932645bf8143cc984cbf1168bf97",
                    flag: 161,
                    type: 162
                }, {
                    PKey: "049923777d866fd80485be57a126d638cc7dda78a5d6958aff784ca7ed9d9c7be494125bf75fd0328490ae51020274427b9fbb07f59e4c9b5104ac6924721a4438",
                    coinbase: "0xa17af10277326021cea21bc8bddece55a17c4585",
                    flag: 161,
                    type: 162
                }]
              }
}
```

***
## Cpm

#### cpm_showGroup
`ShowGroup(addresscommon.Address,blockNrrpc.BlockNumber)(map[string]interface{},error)`

Returns  information about group info.

##### Parameters
1. `DATA`, 20 Bytes - address to show group info.
2. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)

##### Example Parameters
```js
params: [
   '0x1344abe0cf2ed59a80b320574339bbd329fd1f1f',
   'latest'
]
```

##### Returns

  - `BlackManager`: `Array`, black manager member.
  - `BlackMembers`: `Array`, black member info.
  - `Creator`:  `DATA`, 20 Bytes - address of the create root.
  - `GroupKey`:  `DATA`, 20 Bytes - address of the group.
  - `Id`: `QUANTITY`- group index.
  - `WhiteManager`: `Array`, white manager member.
  - `WhiteMembers`: `Array`, white member info.
  - `name`: `Object`, name of group.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"cpm_showGroup","params":["latest"],"id":100}'

// Result
{
  "id":100,
  "jsonrpc":"2.0",
  "result":
        {
          BlackManager: null,
          BlackMembers: null,
          Creator: "0x0000000000000000000000000000000000000001",
          GroupKey: "0x1344abe0cf2ed59a80b320574339bbd329fd1f1f",
          Id: 3,
          WhiteManager: null,
          WhiteMembers: ["0xee7584b00c072e57789d0646f29c328b565b3f37"],
          name: "yan-2"
        }
}
```

***

#### cpm_listBasePermission
`ListBasePermission(addresscommon.Address,blockNrrpc.BlockNumber)(bool,bool,error)`

Returns  information about address send tx and create contract permission.

##### Parameters

1. `DATA`, 20 Bytes - address to check for permission.
2. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)

##### Example Parameters
```js
params: [
   '0xc94770007dda54cF92009BFF0dE90c06F603a09f',
   'latest'
]
```

##### Returns

  - `createContract`: `DATA`, 20 Bytes - bool of the permission of send tx.
  - `sendtransaction`: `DATA`, bool of the permission of create contract.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"cpm_listBasePermission","params":["0xc94770007dda54cF92009BFF0dE90c06F603a09f", "latest"],"id":100}'

// Result
{
  "id":100,
  "jsonrpc":"2.0",
  "result":{
             createContract: true,
             sendtransaction: true
           }
}
```

***

#### cpm_listPermission
`ListPermission(group_contract_Addrcommon.Address,permTypeuint8,blockNr rpc.BlockNumber)map[string]interface{}`

Returns  information about all permission for example 
* all person send tx for number 1
* all person create contract for number 2
* group manager member for number 3

##### Parameters

1. `DATA`, 20 Bytes - address to check for permission.
    - if you want Listgroup write Group address
    - if you want Listcontract make contract address
2. `QUANTITY|TAG` - integer permission  query number,
    - 1 represent all person send tx permission
    - 2 represent all person create contract permission
    - 3 for group 
    - 4  for contract
3. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)

##### Example Parameters
```js
params: [
   '0xc94770007dda54cF92009BFF0dE90c06F603a09f',
   'latest'
]
```

##### Returns

  - `BlackManager`: `Array`, black manager member.
  - `BlackMembers`: `Array`, black member info.
  - `WhiteManager`: `Array`, white manager member.
  - `WhiteMembers`: `Array`, white member info.

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"cpm_listPermission","params":["0xc94770007dda54cF92009BFF0dE90c06F603a09f", "latest"],"id":100}'

// Result
{
  "id":100,
  "jsonrpc":"2.0",
  "result":{
           "WhiteMembers":wmember,
           "WhiteManager":wManager,
           "BlackMembers":bMember,
           "BlackManager":bmanager,
           }
}
```

***

#### cpm_showMyGroup
`ShowMyGroup(addresscommon.Address,blockNrrpc.BlockNumber)([]common.Address,error)`

Returns  information about my ower group list.

##### Parameters

1. `DATA`, 20 Bytes - address to check for balance.
2. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)

##### Example Parameters
```js
params: [
   '0xc94770007dda54cF92009BFF0dE90c06F603a09f',
   'latest'
]
```

##### Returns
   - `address`:  `Array`, 20 Bytes - address of the all groups.
   
##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"cpm_showMyGroup","params":["0xc94770007dda54cF92009BFF0dE90c06F603a09f", "latest"],"id":100}'

// Result
{
  "id":100,
  "jsonrpc":"2.0",
  "result":[{
               address: "0xc02f50f4f41f46b6a2f08036ae65039b2f9acd69",
           }] 
}
```

***

#### cpm_showBlackList
`ShowBlackList(blockNrrpc.BlockNumber)([]common.Address,error)`

Returns  information about black list all member.

##### Parameters

1. `QUANTITY|TAG` - integer block number, or the string `"latest"`, `"earliest"` or `"pending"`, see the [default block parameter](#the-default-block-parameter)

##### Example Parameters
```js
params: [
   'latest'
]
```

##### Returns

   - `member`: `Array`, all black list address.
   
##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"cpm_showBlackList","params":["latest"],"id":100}'

// Result
{
  "id":100,
  "jsonrpc":"2.0",
  "result":{[]common.Address}
}
```