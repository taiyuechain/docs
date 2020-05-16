# DPoS委员会节点参与教程

## 编译Taipublic
根据平台在下面链接中选择安装指导。

* [Mac OS X安装说明](https://github.com/taiyuechain/taipublicchain/wiki/Installation-Instructions-for-Mac-OS-X)
* [Windows安装说明](https://github.com/taiyuechain/taipublicchain/wiki/Installation-Instructions-for-Windows)
* Linux/Unix的安装说明
  * [Ubuntu](https://github.com/taiyuechain/taipublicchain/wiki/Installation-Instructions-for-Ubuntu)
  * [Centos](https://github.com/taiyuechain/taipublicchain/wiki/Installation-Instructions-for-Centos)
* Docker的使用说明
  * [Docker](https://github.com/taiyuechain/taipublicchain/wiki/Running-in-Docker)

或者直接下载[对应平台版本](https://github.com/taiyuechain/taipublicchain/releases)
## 编译Impawn-CLI

taipublic `Impawn CLI` 是一个可以调用质押合约参与pos委员会选举的工具，提供了质押，追加，更新fee，赎回，提取和查询方法。 
[详情](https://github.com/taiyuechain/taipublicchain/wiki/Impawn-CLI).

### 验证节点配置

* `4 CPU`
* `RAM 16G `
* `Storage 200G SSD`
* `Public IP  4Mbps`

### 准备
**`getrue`支持`rpc`**
```
./taipublic  --rpc --rpcaddr 127.0.01 --rpcport 8545 --rpcapi "etrue,net,web3,impawn"  console
```

参数是`--rpcaddr 0.0.0.0`，`getrue`将监听所有的地址,也可以指定一个想要连接的地址，设置`--rpcaddr 127.0.01`仅需要本地连接`getrue`.

**`taipublic`支持`BFT`**
```
./taipublic   --bftip 39.98.251.xx console
```
`bftip`必须是`公网ip`, open `防火墙` 端口 8545(`rpc`),30310(`bftport`),30311(`bftport2`)

**常规启动参数** 
```shell
$ ./taipublic --datadir data  --bftip "39.98.251.xxx" --rpc --rpcaddr "127.0.0.1"  --rpcapi "eth,etrue,net,web3,impawn"  console 
```

## 编译源码
编译`impawn`需要go和c编译器，如果已经安装好依赖, 运行如下命令。

```shell
    cd taipublicchain/cmd/impawn
    go build -o impawn  main.go query_stake.go impawn.go
```

## 运行CLI
 TaiPublic质押流程分为3步，首先保证账户有余额的前提下，发起质押交易[impawn](#质押)，质押量(`value`)要大于2W `true`才可参与委员会竞选,如果
下届准备退出委员会POS共识，在本届发起[cancel](#赎回)交易，等待15天后，需要`主动`发起提取[withdraw](#提取)交易，提取的true会立即到指定的账户。

* 由于[impawn](#质押)需要大于2W才可以调用成功，如果质押量小于2W，可以使用[append](#追加)
* 更新Fee可以调用[更新Fee](#更新Fee)
* 更新验证者PK可以调用[更新PK](#更新PK)
* 使用[查询奖励](#查询奖励)查询余额和奖励信息

### 竞选质押

```bash
$ tree
.
├── impawn
├── impawn.go
├── main.go
├── query_stake.go
├── README.md
└── UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx

$ ./impawn --keystore UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx --rpcaddr 39.100.97.*** --rpcport 8545 --value 20000 --fee 5000
```

命令解释:
 * `--keystore` 加载私钥从UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx文件里面.
 * `--rpcaddr` `--rpcport`  连接节点的ip + port,这个节点必须是一个验证者节点, 将使用本地的bft pk参与委员会竞选.
 * `--value`  质押 **>=20000** true到pos地址, 验证节点才能成为候选委员会节点.
 * `--fee`  fee的范围是(0-10000),值越小，委托者分配的收益越低，值越大，收益越高, 费率的公式为fee / 10000.

**输出日志**
 ```shell
Please enter the password for 'UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxxx': 
Connect url  http://39.100.97.***:8545  current number  4467994  address  0x7C357530174275Dd30E46319B89f71186256E4f7
Your wallet balance is  1.7779439190971997852e+07 'true   current Total Stake  700401
Fee 5000  Pubkey  04f7a84c02fd576545c102d73cee71097813c255d5791cdcb600b82aedbf6f05dfda801e88985b3bfecc21592a7211ad4b551071f0bed8b357ea949e53fc9c5e8c  value  20000000000000000000000
TX data nonce  17  transfer value  20000000000000000000000  gasLimit  826392  gasPrice  1000000  chainID  18928
Please waiting   txHash  0xf1532026e8ffe44a1ea85c5e0772ffb7e6210d2f4bceed15c07078ddb48043a4
Transaction Success  block Number 4467996  block txs 3 blockhash 0xab6af69d64ff17affa2460a7bd39552463611c09eab2cf5a769889d25e5afb96
Staked  20000000000000000000000 wei = 20000 true Locked  0  wei = 0 true Unlocked  0  wei = 0 true
```
  
### 赎回
```
$ ./impawn --keystore UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx --rpcaddr 39.100.97.xxx --rpcport 8545 --value 10  cancel

```

命令解释:
 * `--keystore` 加载私钥从UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx文件里面.
 * `--rpcaddr` `--rpcport`  连接节点的ip + port,这个节点必须是一个验证者节点, 将使用本地的bft pk参与委员会竞选.
 * `--value`  想要赎回true的数量.
 * `cancel`  想要提取true，首先要先赎回(`cancel`), 这个命令是要赎回10个true到锁定状态，可以在下一届开始提取(`withdraw`)，一般是15天后.

**输出日志**
```shell
Please enter the password for 'UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxxx': 
Connect url  http://39.100.97.xxx:8545  current number  4468624  address  0x7C357530174275Dd30E46319B89f71186256E4f7
TX data nonce  19  transfer value  0  gasLimit  821784  gasPrice  1000000  chainID  18928
Please waiting   txHash  0x1bd50e4755cac0b2ae69f080d645c7a78a24c51ad31570f6afcc6f853a820b10
Transaction Success  block Number 4468626  block txs 3 blockhash 0x0248f6467a7d50962115a210e815737bb1d0be5012adc96212cf9b458dc65f05
Staked  4999000000000000000000 wei = 49990 true Locked  10000000000000000000  wei = 10 true Unlocked  0  wei = 0 true
```

### 查询提取高度
```
$ ./impawn --keystore UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx --rpcaddr 39.100.97.xxx --rpcport 8545 querystaking

```

命令解释:
 * `--keystore` 加载私钥从UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx文件里面.
 * `--rpcaddr` `--rpcport`  连接节点的ip + port,这个节点必须是一个验证者节点, 将使用本地的bft pk参与委员会竞选.
 * `querystaking`  `Staked`当前质押的数量, `Locked`进入锁定状态的数量(调用`cancel`后进入这个状态),`Unlocked`可以立即提取的数量.
 * 打印`withdraw`高度, 这个高度后可以发提取交易, 如果`lock` 等于`false`,可以立即提取. 
 * 如果`Unlocked` 不等于0, 可以立即提取Unlocked数量的true.
 
**输出日志**
```shell
Please enter the password for 'UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxxx': 
Connect url  http://39.100.97.xxx:8545  current number  4468689  address  0x7C357530174275Dd30E46319B89f71186256E4f7
Staked  49990000000000000000000 wei = 49990 true Locked  10000000000000000000  wei = 10 true Unlocked  0  wei = 0 true
Your can withdraw after height 4471006  count value  10  true  index 0  lock  true
```

### 提取
*使用[query staking](#查询提取高度) 查询`Unlocked`不为0.*
```shell
Staked  1000000000000000000 wei = 1 true Locked  0  wei = 0 true Unlocked  10000000000000000000  wei = 10 true
```
**可以提取赎回的true**
```
$ ./impawn --keystore UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx --rpcaddr 39.100.97.xxx --rpcport 8545 --value 10 withdraw

```

命令解释:
 * `--keystore` 加载私钥从UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx文件里面.
 * `--rpcaddr` `--rpcport`  连接节点的ip + port,这个节点必须是一个验证者节点, 将使用本地的bft pk参与委员会竞选.
 * `--value`  想要提取true的数量.
 * `withdraw`  子命令表示一笔提取交易到你的地址.

**输出日志**
```shell
Please enter the password for 'UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxxx': 
Connect url  http://39.100.84.72:8545  current number  4501013  address  0x7C357530174275Dd30E46319B89f71186256E4f7
Your wallet balance is  1.7779438190969483348e+07 'true   current Total Stake  700402
TX data nonce  20  transfer value  0  gasLimit  861784  gasPrice  1000000  chainID  18928
Please waiting   txHash  0x659dbaf0a920aceed810647d3e2f113b508e8748dd82d2b0dae067f952214449
Transaction Success  block Number 4501014  block txs 3 blockhash 0x177e1c2af3c6dc1eecc6139c1b438fde86cb5c30f015d611d0191af7e96230de
Staked  1000000000000000000 wei = 1 true Locked  0  wei = 0 true Unlocked  0  wei = 0 true
Your wallet balance is  1.7779448190968621564e+07 'true   current Total Stake  700392
```

### 追加
```
$ ./impawn --keystore UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx --rpcaddr 39.100.97.xxx --rpcport 8545 --value 10 append

```

命令解释:
 * `--keystore` 加载私钥从UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx文件里面.
 * `--rpcaddr` `--rpcport`  连接节点的ip + port,这个节点必须是一个验证者节点, 将使用本地的bft pk参与委员会竞选.
 * `--value`   想要追加true的量，不会更改fee.
 * `append`    子命令已经质押过还要继续质押.

**输出日志**
```shell
Please enter the password for 'UTC--2018-09-07T07-45-16.954721700Z--7c357530174275dd30e46319b89f71186256e4f7': 
Connect url  http://39.100.84.72:8545  current number  4501430  address  0x7C357530174275Dd30E46319B89f71186256E4f7
TX data nonce  22  transfer value  10000000000000000000  gasLimit  821272  gasPrice  1000000  chainID  18928
Please waiting   txHash  0x01a4d6bb8c85113118b47e27373b92dab5914f8103d3a16e46b3b4a65d15bbd3
Transaction Success  block Number 4501432  block txs 1 blockhash 0xf78f0d87e4178e22effd6715999368df8af44c1fea08c401cbd2ed23a9d7ccb8
Staked  11000000000000000000 wei = 11 true Locked  0  wei = 0 true Unlocked  0  wei = 0 true
```

### 更新Fee
```
$ ./impawn --keystore UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx --rpcaddr 39.100.97.xxx --rpcport 8545 --fee 10 updatefee

```

命令解释:
 * `--keystore`   加载私钥从UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx文件里面.
 * `--rpcaddr` `--rpcport`  连接节点的ip + port,这个节点必须是一个验证者节点, 将使用本地的bft pk参与委员会竞选.
 * `--fee`       fee的范围是(0-10000),值越小，委托者分配的收益越低，值越大，收益越高, 费率的公式为fee / 10000.
 * `updatefee`   子命令更新验证者的fee(0-10000),会改变委托者的收益.

**输出日志**
```shell
Please enter the password for 'UTC--2018-09-07T07-45-16.954721700Z--7c357530174275dd30e46319b89f71186256e4f7': 
Connect url  http://39.100.84.72:8545  current number  4503733  address  0x7C357530174275Dd30E46319B89f71186256E4f7
Fee 6000
TX data nonce  25  transfer value  0  gasLimit  821528  gasPrice  1000000  chainID  18928
Please waiting   txHash  0x9ba1a83f8e4a074d311ef24993cc6a3baf82936c6b73f76b77eac95204bfd772
Transaction Success  block Number 4503743  block txs 5 blockhash 0xc3a188dd5da8b47efd239cd0f47fb81ee576242c5c819830cb89fee397fe06fc
```

### 更新PK
```
$ ./impawn --keystore UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx --rpcaddr 39.100.97.xxx --rpcport 8545 --bftkey 647eeeb80193a47a02d31939af29efa006dbe6db45c8806af764c18b262bb90b  updatepk

```

命令解释:
 * `--keystore`   加载私钥从UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx文件里面.
 * `--rpcaddr` `--rpcport`  连接节点的ip + port,这个节点必须是一个验证者节点, 将使用本地的bft pk参与委员会竞选.
 * `--bftkey`   `647eeeb80193a47a02d31939af29efa006dbe6db45c8806af764c18b262bb90b` 私钥或使用`--pubkey`加公钥.
 * `updatepk`   子命令更新验证者的pk,委员会之间通信的标识.

**输出日志**
```shell
Connect url  http://localhost:8545  current number  5048960  address  0xDaa07f97034916517afFF28b672A61B0027346a2
 Pubkey  045772b765ed192fdd53dd4a579dc53e37682bd975001071ff232f8cdad05734cbbdded8d8fb758845d315115f012e136739f6f3e1e9654eff45b36cb06ce8f9f6
TX data nonce  9155  transfer value  0  gasLimit  2426136  gasPrice  1000000000  chainID  18928
Please waiting   txHash  0xe157cbac55796b4a97dd28421fa1621edb562a5b95aadebe5d868879fe51e5e2
Transaction Success  block Number 5048961  block txs 1 blockhash 0xf55332105a203d92df53fc5609e8465dbae5a0ef166e3548b1c25d5c4d6e473a
Staked  100020000000000000000000 wei = 100020 true Locked  0  wei = 0 true Unlocked  0  wei = 0 true
```

### 查询奖励

```
$ ./impawn --keystore UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx --rpcaddr 39.100.97.xxx --rpcport 8545 queryreward

```

命令解释:
 * `--keystore` 加载私钥从UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx文件里面.
 * `--rpcaddr` `--rpcport`  连接节点的ip + port,这个节点必须是一个验证者节点, 将使用本地的bft pk参与委员会竞选.
  * `queryreward`  打印可使用(`valid`)的余额和锁定(`lock`)的余额,每一个慢链块的奖励.
 
**输出日志**
```shell
Please enter the password for 'UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxxx': 
Connect url  http://39.100.97.xxx:8545  current number  4468689  address  0x7C357530174275Dd30E46319B89f71186256E4f7
Your wallet valid balance is  11120.337165556650564 'true   lock balance is  100000 'true
queryRewardInfo [map[Address:0xa4ab123ab418197ab0b5e3c49269f5d530ef87f0 Amount:2.8086168529799127e+18]]
```

### 转账
```
$ ./impawn --keystore UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx --rpcaddr 39.100.97.xxx --rpcport 8545 --value 10 --address 0x3f944d3f12e904e1A647E5FF9f531B8deE2346B2 send 

```

命令解释:
 * `--keystore` 加载私钥从UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx文件里面.
 * `--rpcaddr` `--rpcport`  连接节点的ip + port,这个节点必须是一个验证者节点, 将使用本地的bft pk参与委员会竞选.
 * `--address`  对方的地址.
 * `--value`    转账true的量.
 * `send`       子命令发送普通转账交易.

**输出日志**
```shell
Please enter the password for 'UTC--2018-09-07T07-45-16.954721700Z--xxxxxxxxxx': 
Connect url  http://39.100.84.72:8545  current number  4502701  address  0x7C357530174275Dd30E46319B89f71186256E4f7
Your wallet balance is  1.7779429190966933964e+07 'true   current Total Stake  700411
TX data nonce  23  transfer value  10000000000000000000  gasLimit  21000  gasPrice  1000000  chainID  18928
Please waiting   txHash  0x09b401884282f32f083d75ad537d1b461dc451c77a25e44f2d1fd859410561d0
Transaction Success  block Number 4502702  block txs 5 blockhash 0xc3a188dd5da8b47efd239cd0f47fb81ee576242c5c819830cb89fee397fe06fc
```

### 查询交易执行情况
```
$ ./impawn  --rpcaddr 39.100.97.xxx --rpcport 8545 --txhash 0x40c78769add225421c45fa2e9dc206c1d9a03199f78c34644f3c0bf274f3066b querytx

```

命令解释:
 * `--rpcaddr` `--rpcport`  连接节点的ip + port.
 * `--txhash`   查询交易hash.
 * `querytx`    子命令查询交易hash执行结果.
 
**输出日志**
```
Connect url  http://39.100.84.xxx:8545  current number  4501518  address  0x0000000000000000000000000000000000000000
Transaction Success  block Number 4501432  block txs 1 blockhash 0xf78f0d87e4178e22effd6715999368df8af44c1fea08c401cbd2ed23a9d7ccb8
```