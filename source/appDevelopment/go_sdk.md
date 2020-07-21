## Go SDK

`获取conn连接`,即可调用下面的方法。

```
	conn, err := yueclient.Dial("http://39.100.97.129:8545")
```

### ListPermission
`ListPermission(ctx context.Context, group_contract_Addr common.Address, permType uint8, number *big.Int) (map[string]interface{}, error)`

**说明：** 
这个是列出所有的权限，比如所有人发送交易的权限，比如某个合约，某个组的所有权限人员列表

**参数：**
* blockNr ：表示那个高度的权限
* group_contract_Addr ：
	* 如果想List group就填写Group地址，
	* 如果想List contract 就填写 contract 地址

* permType ：
* 表示：列出所有所有发送交易的人的权限
 * 表示：列出所有创建合约权限的人的权限
* 表示组的
* 表示合约的

**返回值：**
```
fields = map[string]interface{}{
		"WhiteMembers":      wmember,
		"WhiteManager":    wManager,
		"BlackMembers":      bMember,
		"BlackManager": bmanager,
```
### ShowWhiteList
`ShowWhiteList(ctx context.Context, number *big.Int) ([]common.Address, error)`

**描述：**
返回白名单list的所有成员，

**参数：**
blockNr： 表示那个高度的状态 

**返回值：**
```
[]common.Address ： 所有白名单成员
```

### ShowBlackList
`ShowBlackList(ctx context.Context, number *big.Int) ([]common.Address, error)`

**描述：**
返回黑名单list的所有成员

**参数：**
blockNr： 表示那个高度的状态 

**返回值：**
```
[]common.Address ： 所有白名单成员
```

### ShowMyGroup
`ShowMyGroup(ctx context.Context, addr common.Address, number *big.Int) ([]common.Address, error)`

**描述：**

列出我所在的组

**参数：**
blockNr ：多少高度的组管理员
address ：谁

**返回值：**
```
[]common.Address：所有组的地址列表
```

### ShowGroup
`ShowMyGroup(ctx context.Context, addr common.Address, number *big.Int) ([]common.Address, error)`

**描述：**
列出组的相关信息

**参数：**
* blockNr ：哪个高度的
* address ：哪个组

**返回值：**
```
fields := map[string]interface{}{
		"GroupKey":     	pTable.GropPermi[address].GroupKey,
		"Creator":       	pTable.GropPermi[address].Creator,
		"Id": 				pTable.GropPermi[address].Id,
		"name":				pTable.GropPermi[address].Name,
		"WhiteMembers":      wmember,
		"WhiteManager":    wManager,
		"BlackMembers":      bMember,
		"BlackManager": bmanager,
	}
```
	
### ListBasePermission

**描述：**
列出某个人的基础权限

**参数：**
* blockNr ：哪个高度
* address ：哪个地址

**返回值：**
```
Bool：发送交易权限
Bool：创建合于权限
```