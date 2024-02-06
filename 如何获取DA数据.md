# 如何通过Domicon网络查询上传的DA数据


## 查询方法

目前Domicon支持的用户查询上传的DA数据方法有三个：
1.eth_getFileDataByHash 
2.eth_getFileDataByCommitment 
3.eth_batchFileDataByHashes

对于这三种获取DA数据方法的详细说明如下：

### 1.eth_getFileDataByHash

#### 功能描述
通过原始交易哈希获取DA数据

#### 使用场景
用户通过原始的交易哈希获取对于DA数据的查询，无论这个DA数据已经磁盘化还是位于内存池中。

#### 返回值
返回一个对应的DA数据对象，如果没查询到就返回一个空值，DA数据对象结构如下：

- Sender: DA数据的提交者地址
- Submmiter: DA数据的广播者地址
- Length: DA数据的长度
- Index: DA数据的提交者的发送序号
- Commitment: DA数据承诺，承诺由KZG算法生成与Data一一对应
- Data: DA数据
- Sign: DA数据的提交者对于以上所有数据的签名
- TxHash: 原始交易哈希

#### 调用方式
1.方式一

```
curl -H "content-type: application/json" -X POST --data '{"id":0,"jsonrpc":"2.0","method":"eth_getFileDataByHash","params":["0xxxxxxx(交易哈希)"]}' http://xx.xx.xx:8545 （节点的公网地址）

```

2.方式二

```go
	port := "8545"
	client,err := ethclient.DialContext(context.TODO(),"http://xxx.xxx.xx.xxx:" + port)
	if err != nil {
		println("DialContext-----err",err.Error())
	}

	da,err := client.GetFileDataByHash(context.TODO(),common.BytesToHash([]byte("2")))
	if err != nil {
		println("GetFileDataByHash---err",err.Error())
	}

    println("GetFileDataByHash--result---",da)
```


### 2.eth_getFileDataByCommitment

#### 功能描述
通过承诺哈希获取DA数据

#### 使用场景
用户通过承诺获取对于DA数据的查询，只能查询已经磁盘化的DA数据，位于内存池中的数据则无法查询。

#### 返回值
返回一个对应的DA数据对象，如果没查询到就返回一个空值，DA数据对象结构如下：

- Sender: DA数据的提交者地址
- Submmiter: DA数据的广播者地址
- Length: DA数据的长度
- Index: DA数据的提交者的发送序号
- Commitment: DA数据承诺，承诺由KZG算法生成与Data一一对应
- Data: DA数据
- Sign: DA数据的提交者对于以上所有数据的签名
- TxHash: 原始交易哈希

#### 调用方式
1.方式一

```
curl -H "content-type: application/json" -X POST --data '{"id":0,"jsonrpc":"2.0","method":"eth_getFileDataByCommitment","params":["0xxxxxxx(承诺)"]}' http://xx.xx.xx:8545 （节点的公网地址）

```

2.方式二

```go
	port := "8545"
	client,err := ethclient.DialContext(context.TODO(),"http://xxx.xxx.xx.xxx:" + port)
	if err != nil {
		println("DialContext-----err",err.Error())
	}

	da,err := client.GetFileDataByCommitment(context.TODO(),common.Hex2Bytes("0xxxxxxxxxxxxx"))
	if err != nil {
		println("GetFileDataByCommitment---err",err.Error())
	}

    println("GetFileDataByCommitment--result---",da)
```




### 3.eth_batchFileDataByHashes

#### 功能描述
通过批量原始交易哈希获取批量DA数据

#### 使用场景
用户通过原始的交易哈希获取对于DA数据的查询，无论这个DA数据已经磁盘化还是位于内存池中。

#### 返回值
返回一个是否拥有与原始交易哈希相对应的DA数据的bool值列表，true就是有，false就是没有。

#### 调用方式
1.方式一

```
curl -H "content-type: application/json" -X POST --data '{"id":0,"jsonrpc":"2.0","method":"eth_batchFileDataByHashes","params":[TxHashes:["0xxxxxxx(交易哈希1)","0xxxxxx(交易哈希2)"]]}' http://xx.xx.xx:8545 （节点的公网地址）

```

2.方式二

```go
	port := "8545"
	client,err := ethclient.DialContext(context.TODO(),"http://xxx.xxx.xx.xxx:" + port)
	if err != nil {
		println("DialContext-----err",err.Error())
	}

	res,err := client.GetBatchFileDataByHashes(context.TODO(),rpc.TxHashes{TxHashes: []common.Hash{common.BytesToHash([]byte("2"))}})
	if err != nil {
		println("GetBatchFileDataByHashes-----err",err.Error())
	}

    println("GetBatchFileDataByHashes--result---",res)
```

