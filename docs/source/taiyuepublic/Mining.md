# CPU Mining with taipublic
#### CPU_Mining
To mine at taipublicchain, you'll just need taipublicchain client, taipublic. 


_**NOTE:** Ensure your blockchain is fully synchronised with the main chain before starting to mine, otherwise you will not be mining on the main chain._

When you start up your taipublicchain node with `taipublic` it is not mining by default. To start it in mining mode, you use the `--mine` [command line option](https://github.com/taipublicchain/taipublicchain-engineering-code/wiki/Command-Line-Options). The `-minerthreads` parameter can be used to set the number parallel mining threads (defaulting to the total number of processor cores). 

`taipublic --mine --minerthreads=4`

only mine fruit

`taipublic --minefruit --minerthreads=4`

You can also start and stop CPU mining at runtime using the console. `miner.start` takes an optional parameter for the number of miner threads.

```
> miner.start(8)
null
> miner.stop()
true
```
or

```
> miner.startFruit(8)
null
> miner.stop()
true
```

Note that mining for real TRUE only makes sense if you are in sync with the network (since you mine on top of the consensus block). Therefore the taipublicchain downloader/synchroniser will delay mining until syncing is complete, and after that mining automatically starts unless you cancel your intention with `miner.stop()`.

In order to earn TRUE you must have your **coinbase** address set. This coinbase defaults to your [primary account](https://github.com/taiyuechain/taipublicchain/wiki/Managing-your-accounts). If you don't have an coinbase address, then `taipublic --mine` or `taipublic --minefruit`will not start up.

You can set your coinbase on the command line:

```
taipublic --coinbase '0xa4d8e9cae4d04b093aac82e6cd355b6b963fb7ff' --mine 2>> taipublic.log
```

or

```
taipublic --coinbase '0xa4d8e9cae4d04b093aac82e6cd355b6b963fb7ff' --minefruit 2>> taipublic.log
```

You can reset your coinbase on the console too:
```
miner.setCoinbase(etrue.accounts[2])
```

Note that your coinbase does not need to be an address of a local account, just an existing one. 

There is an option to add extra Data (32 bytes only) to your mined blocks. By convention this is interpreted as a unicode string, so you can set your short vanity tag.

```
miner.setExtra("trueminer")
...
debug.printBlock(131805)
BLOCK(be465b020fdbedc4063756f0912b5a89bbb4735bd1d1df84363e05ade0195cb1): Size: 531.00 B TD: 643485290485 {
NoNonce: ee48752c3a0bfe3d85339451a5f3f411c21c8170353e450985e1faab0a9ac4cc
Header:
[
...
        Miner:           a4d8e9cae4d04b093aac82e6cd355b6b963fb7ff
        Number:             131805
        Extra:              trueminer
...
}
```

You can check your hashrate with miner.getHashRate(), the result is in H/s (Hash operations per second).

```
> miner.getHashRate()
30
```

After you successfully mined some blocks, you can check the true balance of your coinbase account. Now assuming your coinbase is a local account:

```
> tai.getBalance(etrue.coinbase).toNumber();
'34698870000000' 
```

In order to spend your earnings you will need to have this account unlocked.

```
> personal.unlockAccount(etrue.coinbase)
Password
true
```

You can check which blocks are mined by a particular miner (address) with the following code snippet on the console:

```
function minedBlocks(lastn, addr) {
  addrs = [];
  if (!addr) {
    addr = etrue.coinbase
  }
  limit = etrue.blockNumber - lastn
  for (i = etrue.blockNumber; i >= limit; i--) {
    if (etrue.getBlock(i).miner == addr) {
      addrs.push(i)
    }
  }
  return addrs
}
// scans the last 1000 blocks and returns the blocknumbers of blocks mined by your coinbase 
// (more precisely blocks the mining reward for which is sent to your coinbase).   
minedBlocks(1000, etrue.coinbase);
//[352708, 352655, 352559]
```

Note that it will happen often that you find a block yet it never makes it to the canonical chain. This means when you locally include your mined block, the current state will show the mining reward credited to your account, however, after a while, the better chain is discovered and we switch to a chain in which your block is not included and therefore no mining reward is credited. Therefore it is quite possible that as a miner monitoring their coinbase balance will find that it may fluctuate quite a bit. 

Mining success depends on the set block difficulty. Block difficulty dynamically adjusts each block in order to regulate the network hashing power to produce a 10 minute blocktime. Your chances of finding a block therefore follows from your hashrate relative to difficulty. The time you need to wait you are expected to find a block can be estimated with the following code:

**INCORRECT...CHECKING**
```
etrue = etrue.getBlock("latest").difficulty/miner.getHashRate(); // estimated time in seconds
Math.floor(etrue / 3600.) + "h " + Math.floor((etrue % 3600)/60) + "m " +  Math.floor(etrue % 60) + "s";
// 1h 3m 30s
```


# GPU mining

***

## Hardware

The GPU miner is implemented in OpenCL，to get openCL for your chipset and platform, try:
* [AMD SDK openCL](http://developer.amd.com/tools-and-sdks/opencl-zone/amd-accelerated-parallel-processing-app-sdk)
* [NVIDIA CUDA openCL](https://developer.nvidia.com/cuda-downloads)

## On Ubuntu
### NVIDIA

```
add-apt-repository ppa:graphics-drivers/ppa
apt-get install nvidia-418 nvidia-418-dev nvidia-opencl-dev nvidia-opencl-icd-418
```

## Mining  Software

The official release of `taipublic` only supports a CPU miner natively. We are working on a [GPU miner](https://github.com/taipublicchain/trueminer), taipublic however can be used in conjunction with `trueminer`, using the standalone miner as workers and `taipublic` as scheduler communicating via [JSON-RPC](https://github.com/taiyuechain/taipublicchain/wiki/RPC-API). 

Trueminer 0n Linux:
```
git clone https://github.com/taipublicchain/taiminer.git
```

## GPU mining with trueminer 
To  miner with `taipublic`:

```
wget https://github.com/taiyuechain/taipublicchain/releases/download/v1.0.2/taipublic-linux-amd64-1.0.2-758c849.tar.gz
tar -zxvf taipublic-linux-amd64-1.0.2-758c849.tar.gz

```
the detail 'taipublic' you can reference [CPU_mine](#CPU_Mining) 


To install and build GPU `taiminer` from source:

```
cd trueminer
mkdir build
cd build
cmake ..
cmake -budid .
make install
```


To install and build CPU `taiminer` from source:

```
cd taiminer
mkdir build
cd build
cmake .. -DETHASHCL=OFF -DBINKERN=OFF -DETHASHCUDA=OFF -DAPICORE=ON -DETHASHCPU=ON
cmake -budid .
make install
```


The detail `taiminer` install  [trueminer readme.md](https://github.com/taiyuechain/taipublicchain/taiminer/blob/master/README.md)

To set up GPU mining you need a coinbase account. It can be an account created locally or remotely. 

### Using taiminer with taipublic  on solo mode 

* start `taipublic` to support remote mining

```
./taipublic  --datadir ./data --config ./data/config  --rpc --rpcaddr 0.0.0.0 --rpcapi "etrue,:net,web3,miner" --mine --remote --coinbase <coinbase> console
```

`taipublic` will listen all ip address when giving `--rpcaddr 0.0.0.0`, you can give the exact ip address that want miner to connect, or `--rpcaddr 127.0.01` only allow the miner running on the host to connect `taipublic`.

`taiminer` communicates with `taipublic` on port 8545 . You also can change port by giving the [rpcport option](https://github.com/taiyuechain/taipublicchain/wiki/Command-Line-Options)  to `taipublic`.

taiminer will find taipublic on any port. Note that you need to set the param with `hostname:port` to connect the `taipublic` . 

Also note that you do **have** need to give `taipublic` the `--mine` option to start the miner , and also need use `--remote` to support remote getwork . 

* taiminer solo mode using CPU

```
taiminer --cpu -P http://hostname:port

```

* taiminer solo mode using GPU 

```
taiminer -G -P http://hostname:port

```

Use `taiminer -H ` get taiminer a full list of available commands.

If the default command `taiminer` does not work, try to specify the OpenCL device with: `--opencl-device X` where X is 0, 1, 2, etc.
When running `taiminer` with `-M` (benchmark), you should see something like:

    Benchmarking on platform: { "platform": "NVIDIA CUDA", "device": "GeForce GTX 750 Ti", "version": "OpenCL 1.1 CUDA" }


    Benchmarking on platform: { "platform": "Apple", "device": "Intel(R) Xeon(R) CPU E5-1620 v2 @ 3.70GHz", "version": "OpenCL 1.2 " }


### Using taiminer with taipublic on stratum mode 

* taiminer stratum mode using CPU
```
taiminer --cpu -P stratum+tcp://WALLET.WORKER@hostname:port
```

* taiminer stratum mode using GPU
```
taiminer -G -P stratum+tcp://WALLET.WORKER@hostname:port
```
`taiminer` use stratum protocl to connect the mining pool , the  **hostname:port** is pool hostname and port

**Note** hashrate info is not available in `taipublic` ,you have use  `taiminer`need add params  `-R`. 

