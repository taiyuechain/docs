# Java SDK


[yueWeb3jSDK](https://github.com/taiyuechain/yueWeb3j)可以支持访问节点、查询节点状态、修改系统设置和发送交易、权限修改等功能。

SDK主要特性包括：

- 提供调用TaiYueChain的Java API

- 支持使用国密算法发送交易

  

## 环境要求

```java
    - Java版本
     JDK1.8 或者以上版本.    
```

## Java应用引入SDK

通过gradle或maven引入SDK到java应用

gradle:

```java
compile group: 'com.taiyuechain', name: 'yueWeb3j', version: '1.1.1.1'
```

maven:

```java
<dependency>
    <groupId>com.taiyuechain</groupId>
    <artifactId>yueWeb3j</artifactId>
    <version>1.1.1.1</version>
</dependency>

```

## 使用SDK

### 关键初始化

```java
//Sdk默认启用国密Sm2如需secp256k1可以初始化时使用
  YueWeb3j.init(0);
  
//如果想初始化Web3j实例  
  Web3j web3j = YueWeb3j.init("节点");
  
//初始化Web3j实例和secp256k1
  Web3j web3j = YueWeb3j.init("节点",0);
```

### 销毁

```java
web3j.shutdown()
```



### 调用SDK Web3j的API

根据Web3j对象调用相关API。示例代码如下：

```
    //通过Web3j对象调用API接口getBlockNumber
    BigInteger blockNumber = web3j.getBlockNumber().send().getBlockNumber();
    System.out.println(blockNumber);
```

### 创建并使用指定外部账户

SDK发送交易需要一个外部账户，下面是随机创建一个外部账户的方法。

```java
Credentials credentials = GenCredential.create();
//账户地址
String address = credentials.getAddress();
//账户私钥 
String privateKey = credentials.getEcKeyPair().getPrivateKey().toString(16);
//账户公钥 
String publicKey = credentials.getEcKeyPair().getPublicKey().toString(16);
```

使用指定的外部账户

```java
//通过指定外部账户私钥使用指定的外部账户
Credentials credentials = Credentials.create(privateKey);
```



## YueWeb3SDK API

YueWeb3SDK API可以查询区块链相关的状态，发送和查询交易信息和修改权限和组信息。

YueWeb3SDK API是由web3j对象调用的TaiYueChain的RPC API，其API名称与RPC API相同，参考[RPC API文档]()。



### web3j体系概述

web3j的功能组织在不同的包中，下图展示了`org.yueWeb3j`主要包之间的依赖关系：

**core**：JSON RPC协议的封装主要由包`org.yueWeb3j.core`实现，它依赖于`org.yueWeb3j.crypto`包提供的密钥与签名相关的功能，以及`org.yueWeb3j.abi`包提供的java/solidity类型映射支持。

**console**：`org.yueWeb3j.console`包实现了一个可以单独运行的命令行程序web3j，我们将使用它来 生成solidity合约的Java封装类，其中，`org.yueWeb3j.codegen`包实现了从abi到java封装类的代码生成。



### 权限

SDK提供对[分布式控制权限]()的支持，权限结构是Erc20持行，function生成在 **SystemConstantFunctionEncoder** 类，具体如下：

```java
/**
 * 添加成员或者删除委员会成员
 *
 * @param senderCert 授权证书的Byte，这个byte必须是解码以后的
 * @param caCert     新入证书Byte
 * @param publicKey  新入证书pk
 * @param address    新入证书地址
 * @param isAdd      添加标记
 * @return 编码后的function
 */
public static String getMultiProposal(byte[] senderCert, byte[] caCert, byte[] publicKey, String address, boolean isAdd)
```

```java
/**
 * 获取组创建function
 *
 * @param groupName 组名字
 * @return 编码后的function
 */
public static String getCreateGroupPermission(String groupName) 
```

```java
/**
 * 获取组删除function
 *
 * @param groupAddress 组名字
 * @return 编码后的function
 */
public static String getDelGroupPermission(String groupAddress)
```

```java
 /**
     * 权限
     *
     * @param name            合约方法
     * @param contractAddr    合约地址
     * @param memberAddr      成员地址
     * @param groupAddr       组地址
     * @param type            权限代码
     * @param whitelistIsWork 是否创建合约
     * @return 编码后的function
     */
    public static String getGrantPermission(String name, String contractAddr, String memberAddr, String groupAddr, Integer type,Boolean whitelistIsWork)
```

### 具体权限

``` java
/**
 * 获取增加交易权限function
 *
 * @param memberOrGroupAddress 成员或组地址
 * @return 编码后的function
 */
public static String getAddSendTxPerm(String memberOrGroupAddress) {
    return getAddGrantPermission(null, memberOrGroupAddress, null,
            Constant.ModifyPermissionType.ModifyPerminType_AddSendTxPerm.ordinal());
}

/**
 * 获取删除交易权限function
 *
 * @param memberOrGroupAddress 成员或组地址
 * @return 编码后的function
 */
public static String getDelSendTxPerm(String memberOrGroupAddress) {
    return getRemoveGrantPermission(null, memberOrGroupAddress, null,
            Constant.ModifyPermissionType.ModifyPerminType_DelSendTxPerm.ordinal());
}

/**
 * 获取添加交易管理权限function
 *
 * @param memberOrGroupAddress 成员或组地址
 * @return 编码后的function
 */
public static String getAddSendTxManagerPerm(String memberOrGroupAddress) {
    return getAddGrantPermission(null, memberOrGroupAddress, null,
            Constant.ModifyPermissionType.ModifyPerminType_AddSendTxManagerPerm.ordinal());
}

/**
 * 获取删除交易管理权限function
 *
 * @param memberOrGroupAddress 成员或组地址
 * @return 编码后的function
 */
public static String getDelSendTxManagerPerm(String memberOrGroupAddress) {
    return getRemoveGrantPermission(null, memberOrGroupAddress, null,
            Constant.ModifyPermissionType.ModifyPerminType_DelSendTxManagerPerm.ordinal());
}

/**
 * 获取添加合约权限function
 *
 * @param memberOrGroupAddress 成员或组地址
 * @return 编码后的function
 */
public static String getAddCrtContractPerm(String memberOrGroupAddress) {
    return getRemoveGrantPermission(null, memberOrGroupAddress, null,
            Constant.ModifyPermissionType.ModifyPerminType_AddCrtContractPerm.ordinal());
}

/**
 * 获取删除合约权限function
 *
 * @param memberOrGroupAddress 成员或组地址
 * @return 编码后的function
 */
public static String getDelCrtContractPerm(String memberOrGroupAddress) {
    return getRemoveGrantPermission(null, memberOrGroupAddress, null,
            Constant.ModifyPermissionType.ModifyPerminType_DelCrtContractPerm.ordinal());
}

/**
 * 获取添加合约管理权限function
 *
 * @param memberOrGroupAddress 成员或组地址
 * @return 编码后的function
 */
public static String getAddCrtContractManagerPerm(String memberOrGroupAddress) {
    return getAddGrantPermission(null, memberOrGroupAddress, null,
            Constant.ModifyPermissionType.ModifyPerminType_AddCrtContractManagerPerm.ordinal());
}

/**
 * 获取删除合约管理权限function
 *
 * @param memberOrGroupAddress 成员或组地址
 * @return 编码后的function
 */
public static String getDelCrtContractManagerPerm(String memberOrGroupAddress) {
    return getRemoveGrantPermission(null, memberOrGroupAddress, null,
            Constant.ModifyPermissionType.ModifyPerminType_DelCrtContractManagerPerm.ordinal());
}


/**
 * 获取添加组管理权限function
 *
 * @param member       成员
 * @param groupAddress 组地址
 * @return 编码后的function
 */
public static String getAddGropManagerPerm(String member, String groupAddress) {
    return getAddGrantPermission(null, member, groupAddress,
            Constant.ModifyPermissionType.ModifyPerminType_AddGropManagerPerm.ordinal());
}

/**
 * 获取删除组管理权限function
 *
 * @param member       成员
 * @param groupAddress 组地址
 * @return 编码后的function
 */
public static String getDelCrtContractPerm(String member, String groupAddress) {
    return getRemoveGrantPermission(null, member, groupAddress,
            Constant.ModifyPermissionType.ModifyPerminType_DelGropManagerPerm.ordinal());
}

/**
 * 获取添加组成员权限
 *
 * @param member       成员
 * @param groupAddress 组地址
 * @return 编码后的function
 */
public static String getAddGropMemberPerm(String member, String groupAddress) {
    return getAddGrantPermission(null, member, groupAddress,
            Constant.ModifyPermissionType.ModifyPerminType_AddGropMemberPerm.ordinal());
}

/**
 * 获取删除合约管理权限function
 *
 * @param member       成员
 * @param groupAddress 组地址
 * @return 编码后的function
 */
public static String getDelGropMemberPerm(String member, String groupAddress) {
    return getRemoveGrantPermission(null, member, groupAddress,
            Constant.ModifyPermissionType.ModifyPerminType_DelGropMemberPerm.ordinal());
}


/**
 * 获取添加合约成员权限function
 *
 * @param member          成员
 * @param contractAddress 组地址
 * @return 编码后的function
 */
public static String getAddContractMemberPerm(String member, String contractAddress) {
    return getAddGrantPermission(contractAddress, member, null,
            Constant.ModifyPermissionType.ModifyPerminType_AddContractMemberPerm.ordinal());
}

/**
 * 获取删除合约成员权限function
 *
 * @param member          成员
 * @param contractAddress 组地址
 * @return 编码后的function
 */
public static String getDelContractMemberPerm(String member, String contractAddress) {
    return getRemoveGrantPermission(contractAddress, member, null,
            Constant.ModifyPermissionType.ModifyPerminType_DelContractMemberPerm.ordinal());
}

/**
 * 获取添加组成员管理权限
 *
 * @param member          成员
 * @param contractAddress 组地址
 * @return 编码后的function
 */
public static String getAddContractManagerPerm(String member, String contractAddress) {
    return getAddGrantPermission(contractAddress, member, null,
            Constant.ModifyPermissionType.ModifyPerminType_AddContractManagerPerm.ordinal());
}

/**
 * 获取删除组成员管理权限
 *
 * @param member          成员
 * @param contractAddress 组地址
 * @return 编码后的function
 */
public static String getDelContractManagerPerm(String member, String contractAddress) {
    return getRemoveGrantPermission(contractAddress, member, null,
            Constant.ModifyPermissionType.ModifyPerminType_DelContractManagerPerm.ordinal());
}

/**
 * 获取添加白名单权限function
 *
 * @param memberOrGroupAddress 成员或组地址
 * @return 编码后的function
 */
public static String getAddWhitListPerm(String memberOrGroupAddress) {
    return getAddGrantPermission(null, memberOrGroupAddress, null,
            Constant.ModifyPermissionType.ModifyPerminType_AddWhitListPerm.ordinal());
}

/**
 * 获取删除白名单权限function
 *
 * @param memberOrGroupAddress 成员或组地址
 * @return 编码后的function
 */
public static String getDelWhitListPerm(String memberOrGroupAddress) {
    return getRemoveGrantPermission(null, memberOrGroupAddress, null,
            Constant.ModifyPermissionType.ModifyPerminType_DelWhitListPerm.ordinal());
}

/**
 * 获取添加黑名单权限function
 *
 * @param memberOrGroupAddress 成员或组地址
 * @return 编码后的function
 */
public static String getAddBlockListPerm(String memberOrGroupAddress) {
    return getAddGrantPermission(null, memberOrGroupAddress, null,
            Constant.ModifyPermissionType.ModifyPerminType_AddBlockListPerm.ordinal());
}

/**
 * 获取删除黑名单权限function
 *
 * @param memberOrGroupAddress 成员或组地址
 * @return 编码后的function
 */
public static String getDelBlockListPerm(String memberOrGroupAddress) {
    return getRemoveGrantPermission(null, memberOrGroupAddress, null,
            Constant.ModifyPermissionType.ModifyPerminType_DelBlockListPerm.ordinal());
}


/**
 * 获取创建合约权限function
 *
 * @param memberOrGroupAddress 成员或组地址
 * @return 编码后的function
 */
public static String getCreateContract(String memberOrGroupAddress) {
    return getRemoveGrantPermission(null, memberOrGroupAddress, null,
            Constant.ModifyPermissionType.PerminType_CreateContract.ordinal());
}
```

### 系统合约ABI

```java
[
  {
      "name": "GrantPermission",
      "outputs": [],
      "inputs": [
      {
          "type": "bytes",
          "name": "CaCert",
          "indexed": false
     }
      ],
      "anonymous": false,
      "type": "event"
     },
  {
      "name": "grantPermission",
      "outputs": [],
      "inputs": [
    {
          "type": "address",
          "name": "ContractAddr"
        },
    {
          "type": "address",
          "name": "Member"
        },
    {
          "type": "address",
          "name": "GropAddr"
        },
    {
          "type": "uint256",
          "name": "MPermType"
        },
    {
          "type": "bool",
          "name": "WhitelistisWork"
        }
      ],
      "constant": false,
      "payable": false,
      "type": "function"
     },
  {
      "name": "revokePermission",
      "outputs": [],
      "inputs": [
    {
          "type": "address",
          "name": "ContractAddr"
        },
    {
          "type": "address",
          "name": "Member"
        },
    {
          "type": "address",
          "name": "GropAddr"
        },
    {
          "type": "uint256",
          "name": "MPermType"
        },
    {
          "type": "bool",
          "name": "WhitelistisWork"
        }
      ],
      "constant": false,
      "payable": false,
      "type": "function"
     },
  {
      "name": "createGroupPermission",
      "outputs": [
      {
          "type": "address",
          "name": "GropAddr"
          }
    ],
      "inputs": [
      {
          "type": "string",
          "name": "GroupName"
        }
      ],
      "constant": false,
      "payable": false,
      "type": "function"
     },
  {
      "name": "delGroupPermission",
      "outputs": [],
      "inputs": [
      {
          "type": "address",
          "name": "GroupAddr"
        }
      ],
      "constant": false,
      "payable": false,
      "type": "function"
     }
]
```



```java
[
  
  {
      "name": "multiProposal",
      "outputs": [],
      "inputs": [
      {
          "type": "bytes",
          "name": "SenderCert"
        },
    {
          "type": "bytes",
          "name": "CaCert"
        },
    {
          "type": "bytes",
          "name": "Pubk"
        },
    {
          "type": "address",
          "name": "CoinAddr"
        },
    {
          "type": "bool",
          "name": "IsAdd"
        }
      ],
      "constant": false,
      "payable": false,
      "type": "function"
     }
]
```

### 交易发送与数据上链

``` java
		//需要上链的数据做16进制编码  	   
		String Data = "0x0000"

		long chainID = 19330;
        Web3j web3j = Web3j.build(new HttpService("http://39.99.195.63:7545"));
        Credentials credentials = Credentials.create("7631a11e9d28563cdbcf96d581e4b9a19e53ad433a53c25a9f18c74ddf492f75");
        BigInteger nonce = getNonce(credentials.getAddress(), web3j);
        RawTransaction rawTransaction = RawTransaction.createTransaction(nonce, new BigInteger("1000000000"), new BigInteger("21000"),credentials.getAddress(), BigInteger.ONE, data); //传入上链数据data 
 		RawTransaction rawTransaction = RawTransaction.createTransaction(nonce, new BigInteger("1000000000"), new BigInteger("21000"),credentials.getAddress(), BigInteger.ONE,  "0x"); //无上链数据传入0x 
        byte[] signedMessage = TransactionEncoder.signMessage(rawTransaction, chainID, credentials);
        String hexValue = Numeric.toHexString(signedMessage);
        try {
            YueSendTransaction result = web3j.yueSendRawTransaction(hexValue).send();
            System.out.println(result.getTransactionHash());
        } catch (IOException e) {
            e.printStackTrace();
        }
```



## 更多支持

### Rpc文档

### Git官网

https://github.com/taiyuechain

### 官网

https://www.taiyuechain.com/
