# ShowMAN-服务接口V1.0.0 - 精简版

## 修订信息

|       版本	|       时间      |       修订人     |       修订内容        |
|---------------|----------------|-------------------|-------------------    |
|	1.0.0		|	2020-06-05	 |		kyle   		 |		创建文档		 |
---

版权声明 - 本文档所有权归ShowPay，最终解释权归ShowPay所有
[TOC]

## 1 概述

    本文档编写目的为MetaShow公开的服务。


## 2 请求示例

|	地址名称		|	请求地址					|
|-------------------|-------------------------|
|        URL地址           |    https://api.showmoney.app/metaShow |

	GET - 请求示例：
	
	http://XXX.XXX.XXX/XXX/api/v1/XXX/XXX/XXX
	
	响应示例：
	
	```json
	
	{
	    "code":200, 			    // 业务响应状态码
		"msg":"success",            // 业务响应信息，包括成功/失败信息
	    "result":{				    // 响应数据实体
	       ...
	    },
	    "time":1537509332996,	    // 响应时间戳，单位/毫秒
	    "error":null,	            // 业务错误信息
	}
	```



## 3 功能API模块

### 3.1 ShowMetanetData接口

#### 3.1.1 query查询 `/api/v1/query/queryFindMetaData/<content>`  ***GET*** ***Base64URLEncode***

	请求协议：HTTP GET
	
	功能简介：query查询。用url 的 base64


************************************************ 请求参数 ************************************************


|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| find       | map[string]interface 	 | 	否           |	    			    |     查询条件           |
| skip       | int64 	 | 	是      	 |	    			    | 数据偏移量			                |
| limit      | int64 	 | 	是      	 |	    			    | 数据限制量，**默认10，负数为无限制**	    |
| sort       | map[string]int 	 | 	是      	 |	    			    | 排序，-1为倒序，1为顺序		  |
| format     | map[string]string 	 | 	是      	 |	    			    | 返回格式			                |

************************************************ 响应参数 ************************************************

***data***
|	参数名称	   |	类型		|	是否可空	|	长度限制			|	描述				    |
|------------------|----------------|---------------|-----------------------|---------------------------|
| page             | int64 	        | 	否      	|	    		        | 当前页数			        |
| pageSize         | int64 	        | 	否      	|	    		        | 页容量			        |
| total    	       | int64  	    | 	否      	|	    			    | 数据总量    			    |
| data    	       | []map[string]string    | 	否      	|	    			    | 数据    			        |

***ShowMetaData***

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| metanetId           | string 	 | 	否      	 |	    			    | metanet ID		                    |
| rootTxId        | string 	 | 	否      	 |	    			    | 所属顶点TxId			|
| txId        | string 	 | 	否      	 |	    			    | 交易id			|
| vouts        | []*MetaTxOut 	 | 	否      	 |	    			    | vouts			|
| parts          | []string 	 | 	是      	 |	    			    | metanet 的数据			            |
| address   | string 	     | 	是      	 |	    			    | address			        |
| publicKey          | string 	 | 	是      	 |	    			    | publicKey			                |
| parentTxTd   | string 	     | 	否      	 |	    			    | 父txId			            |
| metaId        | string 	 | 	否      	 |	    			    | metaId tag			                |
| nodeName | string 	     | 	否      	 |	    			    | 协议名称			        |
| data      | interface 	 | 	否      	 |	    			    | 数据			        |
| encrypt      | string 	 | 	否      	 |	    			    | 加密方式			        |
| version      | string 	 | 	否      	 |	    			    | 版本			        |
| dataType      | string 	 | 	否      	 |	    			    | 数据类型			        |
| encoding      | string 	 | 	否      	 |	    			    | 编码格式			        |
| blockHeight      | int64 	 | 	否      	 |	    			    | 所在块高			        |
| timestamp         | int64 	 | 	否      	 |	    			    | 时间戳			    |
| isValid         | bool 	 | 	否      	 |	    			    | 是否有效			    |
| isNew         | bool 	 | 	否      	 |	    			    | 是否最新			    |
| fee         | uint64 	 | 	否      	 |	    			    | 该meta数据的费用			    |

***MetaTxOut***

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| txId           | string 	 | 	否      	 |	    			    | 交易id		                    |
| index          | uint64 	 | 	否      	 |	    			    | 索引			                    |
| address        | string 	 | 	是      	 |	    			    | 地址			                    |
| value          | uint64 	 | 	否      	 |	    			    | 金额			                    |
| scriptPubKey   | string 	 | 	否      	 |	    			    | 脚本			                    |
| type           | string 	 | 	否      	 |	    			    | 类型			                    |

************************************************ 请求响应实例 ************************************************	

```json
api请求数据: 
    `{"find":{"data.content":"这是一个测试内容"}, "skip":0, "limit":1}` => Base64URLEncode =>
    
    http://test.showmoney.app/metaShow/api/v1/query/queryFindMetaData/eyJmaW5kIjp7ImRhdGEuY29udGVudCI6Iui_meaYr-S4gOS4qua1i-ivleWGheWuuSJ9LCAic2tpcCI6MCwgImxpbWl0IjowfQ==

响应数据：
 {
  "result": {
    "page": 0,
    "pageSize": 0,
    "total": 2,
    "data": [
      {
        "metanetId": "",
        "txId": "487aa4deecaa5eabd24d7dfb97ded646e71503b26ac9100ff411822459b28daa",
        "vouts": [
          {
            "txId": "487aa4deecaa5eabd24d7dfb97ded646e71503b26ac9100ff411822459b28daa",
            "index": 0,
            "address": "",
            "value": 0,
            "scriptPubKey": "006a046d657461223132634c72757371777571365761727970327535626d765a366a736b59416e6232574066363738373232383230623861613831333662663666343132323864386536663439383363373734376631346230313461363164663264643264316134316662064d6574614944223132634c72757371777571365761727970327535626d765a366a736b59416e623257417b22636f6e74656e74223a22e8bf99e698afe4b880e4b8aae6b58be8af95e58685e5aeb9222c2263726561746554696d65223a313538373631303632323132337d013004302e30390a746578742f706c61696e055554462d38",
            "type": "NullData"
          },
          {
            "txId": "487aa4deecaa5eabd24d7dfb97ded646e71503b26ac9100ff411822459b28daa",
            "index": 1,
            "address": "1J7e9Y6jTPnDoCkfFsmvzxketgDCf8Km7X",
            "value": 2183,
            "scriptPubKey": "76a914bbbba49b5ba95f9fcbf1f2a1b325999fc357963f88ac",
            "type": "P2PKH"
          }
        ],
        "parts": [
          "OP_0",
          "OP_RETURN",
          "meta",
          "12cLrusqwuq6Waryp2u5bmvZ6jskYAnb2W",
          "f678722820b8aa8136bf6f41228d8e6f4983c7747f14b014a61df2dd2d1a41fb",
          "MetaID",
          "12cLrusqwuq6Waryp2u5bmvZ6jskYAnb2W",
          "{\"content\":\"这是一个测试内容\",\"createTime\":1587610622123}",
          "0",
          "0.09",
          "text/plain",
          "UTF-8"
        ],
        "address": "12cLrusqwuq6Waryp2u5bmvZ6jskYAnb2W",
        "publicKey": "NULL",
        "parentTxTd": "f678722820b8aa8136bf6f41228d8e6f4983c7747f14b014a61df2dd2d1a41fb",
        "metaId": "MetaID",
        "nodeName": "12cLrusqwuq6Waryp2u5bmvZ6jskYAnb2W",
        "data": {
          "content": "这是一个测试内容",
          "createTime": 1587610622123
        },
        "encrypt": "0",
        "version": "0.09",
        "dataType": "text/plain",
        "encoding": "UTF-8",
        "blockHeight": 631827,
        "timestamp": 1587633554
      },
      {
        "metanetId": "53d2a9e3437b45933a3a37ffb81d23a81724d50649aea0afc8ff3c30a34fad84",
        "txId": "87b06ecfa3783a41c34235c1846b9f6daee773be7d74d65e482f6805b43b7422",
        "vouts": [
          {
            "txId": "87b06ecfa3783a41c34235c1846b9f6daee773be7d74d65e482f6805b43b7422",
            "index": 0,
            "address": "",
            "value": 0,
            "scriptPubKey": "006a046d657461423033666230316131363533396639613635633265303865353439616134393862643238623133373032613434653762663931313865623366646235633132653630374065393935626265623734646130353839303065396665633432653164336265343636383962376235656530633338393963343833613932323933323361663962064d657461494442303366623031613136353339663961363563326530386535343961613439386264323862313337303261343465376266393131386562336664623563313265363037417b22636f6e74656e74223a22e8bf99e698afe4b880e4b8aae6b58be8af95e58685e5aeb9222c2263726561746554696d65223a313538373631303632323132337d013004302e30390a746578742f706c61696e055554462d38",
            "type": "NullData"
          },
          {
            "txId": "87b06ecfa3783a41c34235c1846b9f6daee773be7d74d65e482f6805b43b7422",
            "index": 1,
            "address": "1J7e9Y6jTPnDoCkfFsmvzxketgDCf8Km7X",
            "value": 1677,
            "scriptPubKey": "76a914bbbba49b5ba95f9fcbf1f2a1b325999fc357963f88ac",
            "type": "P2PKH"
          }
        ],
        "parts": [
          "OP_0",
          "OP_RETURN",
          "meta",
          "03fb01a16539f9a65c2e08e549aa498bd28b13702a44e7bf9118eb3fdb5c12e607",
          "e995bbeb74da058900e9fec42e1d3be46689b7b5ee0c3899c483a9229323af9b",
          "MetaID",
          "03fb01a16539f9a65c2e08e549aa498bd28b13702a44e7bf9118eb3fdb5c12e607",
          "{\"content\":\"这是一个测试内容\",\"createTime\":1587610622123}",
          "0",
          "0.09",
          "text/plain",
          "UTF-8"
        ],
        "address": "12cLrusqwuq6Waryp2u5bmvZ6jskYAnb2W",
        "publicKey": "03fb01a16539f9a65c2e08e549aa498bd28b13702a44e7bf9118eb3fdb5c12e607",
        "parentTxTd": "e995bbeb74da058900e9fec42e1d3be46689b7b5ee0c3899c483a9229323af9b",
        "metaId": "MetaID",
        "nodeName": "03fb01a16539f9a65c2e08e549aa498bd28b13702a44e7bf9118eb3fdb5c12e607",
        "data": {
          "content": "这是一个测试内容",
          "createTime": 1587610622123
        },
        "encrypt": "0",
        "version": "0.09",
        "dataType": "text/plain",
        "encoding": "UTF-8",
        "blockHeight": 632379,
        "timestamp": 1587951949
      }
    ]
  },
  "code": 200,
  "msg": "success",
  "time": 1589189378703,
  "error": "null"
}
```

带返回格式的：
返回格式按照gjson路径格式：

    路径解析
    路径是一系列被.分隔的key拼接而成.
    路径可能包含通配符'*'和'?'.
    通过下标访问数组值.
    通过'#'来获取值在元素中的排位或访问子路径.
    .和通配符可以通过'\'来转义.
    你同样能通过#[...]来查询数组中的第一个匹配的项, 或通过'#[...]#'查询所有匹配的项.
    查询支持==, !=, <, <=, >, >=比较运算符和'%'模糊匹配.

例如：

```
api请求数据: 
    `{"find":{"metaId":"TestShowID","nodeName":"ShowText"}, "skip":0, "limit":0, 
    "format":{"myTag":"metaId","have":"data","myIn":"data.content","h":"blockHeight", "t":"timestamp" ,"address of out":"vouts.0.address"}}` => Base64URLEncode =>
    
    http://test.showmoney.app/metaShow/api/v1/query/queryFindMetaData/eyJmaW5kIjp7Im1ldGFJZCI6IlRlc3RTaG93SUQiLCJub2RlTmFtZSI6IlNob3dUZXh0In0sICJza2lwIjowLCAibGltaXQiOjAsICJmb3JtYXQiOnsibXlUYWciOiJtZXRhSWQiLCJoYXZlIjoiZGF0YSIsIm15SW4iOiJkYXRhLmNvbnRlbnQiLCJoIjoiYmxvY2tIZWlnaHQiLCAidCI6InRpbWVzdGFtcCIgLCJhZGRyZXNzIG9mIG91dCI6InZvdXRzLjAuYWRkcmVzcyJ9fQ==

响应数据：
{
  "result": {
    "page": 0,
    "pageSize": 0,
    "total": 10,
    "data": [
      {
        "address of out": "15b5g9trRPpCBygtyFqXFWxwmH1iksV8tE",
        "h": "631962",
        "have": "000000000000",
        "myIn": "",
        "myTag": "TestShowID",
        "t": 1587713749118
      },
      {
        "address of out": "1HyBrokj77qS5dDQTTAXi14KTBhVJp8TT1",
        "h": "632243",
        "have": "000000000000",
        "myIn": "",
        "myTag": "TestShowID",
        "t": 1587874038054
      },
      {
        "address of out": "1AfeGEqwfg2e6jXCtq66LHprhZdN2YUSja",
        "h": "632383",
        "have": "{\"content\":\"ShowText test data\"}",
        "myIn": "ShowText test data",
        "myTag": "TestShowID",
        "t": 1587957048472
      },
      {
        "address of out": "1HqFY514e4BHJWhoLQSAYt8PApyt6S3iuX",
        "h": "632406",
        "have": "000000000001",
        "myIn": "",
        "myTag": "TestShowID",
        "t": 1587986958930
      },
      {
        "address of out": "1AESm8paj4uUYTqyPEsjSM1w3bfWRFRfw1",
        "h": "632406",
        "have": "{\"content\":\"ShowText test data\"}",
        "myIn": "ShowText test data",
        "myTag": "TestShowID",
        "t": 1587986959013
      },
      ...
    ]
  },
  "code": 200,
  "msg": "success",
  "time": 1590030882788,
  "error": "null"
}
```

-------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------

#### 3.1.2 获取MetaID的Info `/api/v1/query/getMetaIDInfo/<rootTxId>`  ***GET*** 

	请求协议：HTTP GET
	
	功能简介：获取MetaID的Info


************************************************ 请求参数 ************************************************


|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| rootTxId       | string 	 | 	否           |	    			    |     MetaID           |

************************************************ 响应参数 ************************************************

***data***
|	参数名称	   |	类型		|	是否可空	|	长度限制			|	描述				    |
|------------------|----------------|---------------|-----------------------|---------------------------|
| metaIdTag        | string 	    | 	否      	|	    		        | metaId标识			        |
| infoTxId         | string 	    | 	否      	|	    		        | info的TxId			        |
| protocolTxId     | string  	    | 	否      	|	    			    | protocol的TxId    			    |
| name    	       | string         | 	否      	|	    			    | 名称    			        |
| email    	       | string         | 	否      	|	    			    | Email    			        |
| phone    	       | string         | 	否      	|	    			    | 手机号    			        |
| avatar    	   | string         | 	否      	|	    			    | 头像，hexString    			        |

************************************************ 请求响应实例 ************************************************	

```json
api请求数据: 
    http://test.showmoney.app/metaShow/api/v1/query/getMetaIDInfo/a717f2b8364ddab277216408230b1485d28ed3a0bd4b00ab7c7b2437fe58af2e

响应数据：
 {
  "result": {
    "metaIdTag": "TestShowID",
    "infoTxId": "2e8ae6892b9b3873dcaa9d2f03a00325813cdc2c0e739856c1df622ed9c21090",
    "protocolTxId": "9e7f51a6af7d7c760ca003a4fd984987974d02a3b4cc8ba4042f8a16871654ba",
    "name": "Mark42",
    "email": "",
    "phone": "42494531037803de4a6378a98bf5f3164c830ff9a28c59684071146c54a7c56e052c795e4b492aa9647bd975b7988c0c046df3ce75cfe6fae6457f55b5992b62ea5dd74ff21a6f81f6787ff490dc6a683b9a34144599d13177372d5aa4c01ea967871dc3ca",
    "avatar": "..."
  },
  "code": 200,
  "msg": "success",
  "time": 1591329356028,
  "error": "null"
}
```

-------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------

### 3.2 Metanet接口

**暂时只支持和Metaid相关数据**

#### 3.2.1 获取节点 `/api/v1/metanet/getNode/<txId>`

	请求协议：HTTP GET
	
	功能简介：获取节点

************************************************ 请求参数 ************************************************

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| txId          | string 	 | 	否           |	    			    |     txId           |

************************************************ 响应参数 ************************************************

***data***

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| nodeTxId          | int64 	 | 	否           |	    			    | 节点txId                        |
| nodeAddress       | string 	 | 	否      	 |	    			    | 节点地址		                    |
| nodePublicKey     | string 	 | 	否      	 |	    			    | 节点公钥			|
| parentTxId        | string 	 | 	否      	 |	    			    | 父节点txId			|
| parentAddress     | string 	 | 	否      	 |	    			    | 父节点地址			|
| parentPublicKey   | string 	 | 	否      	 |	    			    | 父节点公钥			|
| outputIndex       | int64 	 | 	否      	 |	    			    | 所在索引			|
| blockHeight       | int64 	 | 	否      	 |	    			    | 块高			        |
| rootTxId          | string 	 | 	否      	 |	    			    | 根节点txId			|
| rootAddress       | string 	 | 	否      	 |	    			    | 根节点地址			|
| rootPublicKey     | string 	 | 	否      	 |	    			    | 根节点公钥			|
| timestamp         | int64 	 | 	否      	 |	    			    | 时间戳			    |

************************************************ 请求响应实例 ************************************************	

```json
api请求数据: 
    http://test.showmoney.app/metaShow/api/v1/metanet/getNode/9f0fa21bfe7706fe51decd468069cd8610d7ceb1a1265f2e17559b75d95cc93c
    
响应数据：
{
  "result": {
    "nodeTxId": "9f0fa21bfe7706fe51decd468069cd8610d7ceb1a1265f2e17559b75d95cc93c",
    "nodeAddress": "1KrXEiKZtri9DnndD1MVDG5e1yXA5HNChn",
    "nodePublicKey": "NULL",
    "parentTxId": "c37ee0eef4a98a192c42f28d8c66d3b10bd07a4c84d6a50445c9c9674b1179ed",
    "parentAddress": "1GimPAbPAkmexbbdWqe9fQCQpgZdGNdjy7",
    "parentPublicKey": "",
    "outputIndex": 0,
    "blockHeight": 631827,
    "rootTxId": "8e9b396eb52752c95cfd45b86f9aa90e07e804ac38ff7f7f87669b0af2f06c86",
    "rootAddress": "13DQH5o2WwH72ojKi2GRQAhUuEBUs4euhs",
    "rootPublicKey": "NULL",
    "timestamp": 1587633554062
  },
  "code": 200,
  "msg": "success",
  "time": 1590031471614,
  "error": "null"
}
```

-------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------

#### 3.2.2 获取parts `/api/v1/metanet/getParts/<txId>` 

	请求协议：HTTP GET
	
	功能简介：获取parts

************************************************ 请求参数 ************************************************

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| txId          | string 	 | 	否           |	    			    |     txId           |

************************************************ 响应参数 ************************************************

***data***

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| txId              | string 	 | 	否           |	    			    | 节点txId                        |
| outputIndex       | int64 	 | 	否      	 |	    			    | 所在索引			|
| blockHeight       | int64 	 | 	否      	 |	    			    | 块高			        |
| raw               | string 	 | 	否      	 |	    			    | 脚本			|
| parts             | []string 	 | 	否      	 |	    			    | 解析后的parts			|

************************************************ 请求响应实例 ************************************************	

```json
api请求数据: 
    http://test.showmoney.app/metaShow/api/v1/metanet/getParts/9f0fa21bfe7706fe51decd468069cd8610d7ceb1a1265f2e17559b75d95cc93c
    
响应数据：
 {
  "result": {
    "txId": "9f0fa21bfe7706fe51decd468069cd8610d7ceb1a1265f2e17559b75d95cc93c",
    "blockHeight": 631827,
    "outputIndex": 0,
    "raw": "006a046d65746122314b725845694b5a74726939446e6e6444314d56444735653179584135484e43686e4063333765653065656634613938613139326334326632386438633636643362313062643037613463383464366135303434356339633936373462313137396564064d6574614944046e616d6505416c696365013004302e30390a746578742f706c61696e055554462d38",
    "parts": [
      "OP_0",
      "OP_RETURN",
      "meta",
      "1KrXEiKZtri9DnndD1MVDG5e1yXA5HNChn",
      "c37ee0eef4a98a192c42f28d8c66d3b10bd07a4c84d6a50445c9c9674b1179ed",
      "MetaID",
      "name",
      "Alice",
      "0",
      "0.09",
      "text/plain",
      "UTF-8"
    ]
  },
  "code": 200,
  "msg": "success",
  "time": 1588077699845,
  "error": "null"
}
```

-------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------

#### 3.2.3 获取根节点 `/api/v1/metanet/getRoot/<txId>` 

	请求协议：HTTP GET
	
	功能简介：获取根节点

************************************************ 请求参数 ************************************************

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| txId          | string 	 | 	否           |	    			    |     txId           |

************************************************ 响应参数 ************************************************

***data***

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| txId              | string 	 | 	否           |	    			    | 节点txId                        |
| rootTxId          | string 	 | 	否      	 |	    			    | 根节点txId			|
| rootAddress       | string 	 | 	否      	 |	    			    | 根节点地址			|
| rootPublicKey     | string 	 | 	否      	 |	    			    | 根节点公钥			|

************************************************ 请求响应实例 ************************************************	

```json
api请求数据: 
    http://test.showmoney.app/metaShow/api/v1/metanet/getRoot/9f0fa21bfe7706fe51decd468069cd8610d7ceb1a1265f2e17559b75d95cc93c
    
响应数据：
 {
  "result": {
    "nodeTxId": "9f0fa21bfe7706fe51decd468069cd8610d7ceb1a1265f2e17559b75d95cc93c",
    "rootTxId": "8e9b396eb52752c95cfd45b86f9aa90e07e804ac38ff7f7f87669b0af2f06c86",
    "rootAddress": "13DQH5o2WwH72ojKi2GRQAhUuEBUs4euhs",
    "rootPublicKey": "NULL"
  },
  "code": 200,
  "msg": "success",
  "time": 1588131611869,
  "error": "null"
}
```

-------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------

#### 3.2.4 获取子节点 `/api/v1/metanet/getChildren/<txId>` 

	请求协议：HTTP GET
	
	功能简介：获取子节点

************************************************ 请求参数 ************************************************

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| txId          | string 	 | 	否           |	    			    |     txId           |

************************************************ 响应参数 ************************************************

***data***

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| nodeTxId          | int64 	 | 	否           |	    			    | 节点txId              |
| nodeAddress       | string 	 | 	否      	 |	    			    | 节点地址		        |
| nodePublicKey     | string 	 | 	否      	 |	    			    | 节点公钥			    |
| parentTxId        | string 	 | 	否      	 |	    			    | 父节点txId			|
| parentAddress     | string 	 | 	否      	 |	    			    | 父节点地址			|
| parentPublicKey   | string 	 | 	否      	 |	    			    | 父节点公钥			|
| outputIndex       | int64 	 | 	否      	 |	    			    | 所在索引			    |
| blockHeight       | int64 	 | 	否      	 |	    			    | 块高			        |
| timestamp         | int64 	 | 	否      	 |	    			    | 时间戳			    |

************************************************ 请求响应实例 ************************************************	

```json
api请求数据: 
    http://test.showmoney.app/metaShow/api/v1/metanet/getChildren/8e9b396eb52752c95cfd45b86f9aa90e07e804ac38ff7f7f87669b0af2f06c86
    
响应数据：
{
  "result": [
    {
      "nodeTxId": "c37ee0eef4a98a192c42f28d8c66d3b10bd07a4c84d6a50445c9c9674b1179ed",
      "nodeAddress": "1GimPAbPAkmexbbdWqe9fQCQpgZdGNdjy7",
      "nodePublicKey": "NULL",
      "parentTxId": "8e9b396eb52752c95cfd45b86f9aa90e07e804ac38ff7f7f87669b0af2f06c86",
      "parentAddress": "13DQH5o2WwH72ojKi2GRQAhUuEBUs4euhs",
      "parentPublicKey": "",
      "outputIndex": 0,
      "blockHeight": 631827,
      "timestamp": 1588043791083
    },
    {
      "nodeTxId": "e24fd7d979e73528707ed8af267e5d453bb8cf65e5cb51a04234347e9d27c539",
      "nodeAddress": "196iPAgmCyFRtt4MsdKvtcKZDVRpMdKFMc",
      "nodePublicKey": "NULL",
      "parentTxId": "8e9b396eb52752c95cfd45b86f9aa90e07e804ac38ff7f7f87669b0af2f06c86",
      "parentAddress": "13DQH5o2WwH72ojKi2GRQAhUuEBUs4euhs",
      "parentPublicKey": "",
      "outputIndex": 0,
      "blockHeight": 631827,
      "timestamp": 1588043791086
    }
  ],
  "code": 200,
  "msg": "success",
  "time": 1588226921645,
  "error": "null"
}
```

-------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------

#### 3.2.5 获取节点树 `/api/v1/metanet/getTree/<txId>` 

	请求协议：HTTP GET
	
	功能简介：获取节点树

************************************************ 请求参数 ************************************************

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| txId          | string 	 | 	否           |	    			    |     txId           |

************************************************ 响应参数 ************************************************

***data***

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| txId              | string 	    | 	否           |	    			    | 节点txId                        |
| deep              | int64 	    | 	否           |	    			    | 树总层数                        |
| nodeTotal         | int64 	    | 	否           |	    			    | 树总节点数                        |
| nodeTree          | []*NodeTree 	| 	是      	 |	    			    | 树结构			|

***NodeTree***

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| nodeTxId          | int64 	 | 	否           |	    			    | 节点txId              |
| nodeAddress       | string 	 | 	否      	 |	    			    | 节点地址		        |
| nodePublicKey     | string 	 | 	否      	 |	    			    | 节点公钥			    |
| parentTxId        | string 	 | 	否      	 |	    			    | 父节点txId			|
| parentAddress     | string 	 | 	否      	 |	    			    | 父节点地址			|
| parentPublicKey   | string 	 | 	否      	 |	    			    | 父节点公钥			|
| outputIndex       | int64 	 | 	否      	 |	    			    | 所在索引			    |
| blockHeight       | int64 	 | 	否      	 |	    			    | 块高			        |
| timestamp         | int64 	 | 	否      	 |	    			    | 时间戳			    |
| isSelf            | bool 	     | 	否      	 |	    			    | 是否所查询的txId自己	|
| children          | []*NodeTree| 	是      	 |	    			    | 树结构		    	|

************************************************ 请求响应实例 ************************************************	

```json
api请求数据: 
    http://test.showmoney.app/metaShow/api/v1/metanet/getTree/8e9b396eb52752c95cfd45b86f9aa90e07e804ac38ff7f7f87669b0af2f06c86
    
响应数据：
{
  "result": {
    "txId": "8e9b396eb52752c95cfd45b86f9aa90e07e804ac38ff7f7f87669b0af2f06c86",
    "deep": 4,
    "nodeTotal": 5,
    "nodeTree": {
      "nodeTxId": "8e9b396eb52752c95cfd45b86f9aa90e07e804ac38ff7f7f87669b0af2f06c86",
      "nodeAddress": "13DQH5o2WwH72ojKi2GRQAhUuEBUs4euhs",
      "nodePublicKey": "NULL",
      "parentTxId": "NULL",
      "parentAddress": "NULL",
      "parentPublicKey": "NULL",
      "outputIndex": 0,
      "blockHeight": 631827,
      "timestamp": 1587633554015,
      "isSelf": true,
      "children": [
        {
          "nodeTxId": "c37ee0eef4a98a192c42f28d8c66d3b10bd07a4c84d6a50445c9c9674b1179ed",
          "nodeAddress": "1GimPAbPAkmexbbdWqe9fQCQpgZdGNdjy7",
          "nodePublicKey": "NULL",
          "parentTxId": "8e9b396eb52752c95cfd45b86f9aa90e07e804ac38ff7f7f87669b0af2f06c86",
          "parentAddress": "13DQH5o2WwH72ojKi2GRQAhUuEBUs4euhs",
          "parentPublicKey": "NULL",
          "outputIndex": 0,
          "blockHeight": 631827,
          "timestamp": 1587633554055,
          "isSelf": false,
          "children": [
            {
              "nodeTxId": "9f0fa21bfe7706fe51decd468069cd8610d7ceb1a1265f2e17559b75d95cc93c",
              "nodeAddress": "1KrXEiKZtri9DnndD1MVDG5e1yXA5HNChn",
              "nodePublicKey": "NULL",
              "parentTxId": "c37ee0eef4a98a192c42f28d8c66d3b10bd07a4c84d6a50445c9c9674b1179ed",
              "parentAddress": "1GimPAbPAkmexbbdWqe9fQCQpgZdGNdjy7",
              "parentPublicKey": "NULL",
              "outputIndex": 0,
              "blockHeight": 631827,
              "timestamp": 1587633554062,
              "isSelf": false,
              "children": null
            }
          ]
        },
        {
          "nodeTxId": "e24fd7d979e73528707ed8af267e5d453bb8cf65e5cb51a04234347e9d27c539",
          "nodeAddress": "196iPAgmCyFRtt4MsdKvtcKZDVRpMdKFMc",
          "nodePublicKey": "NULL",
          "parentTxId": "8e9b396eb52752c95cfd45b86f9aa90e07e804ac38ff7f7f87669b0af2f06c86",
          "parentAddress": "13DQH5o2WwH72ojKi2GRQAhUuEBUs4euhs",
          "parentPublicKey": "NULL",
          "outputIndex": 0,
          "blockHeight": 631827,
          "timestamp": 1587633554058,
          "isSelf": false,
          "children": [
            {
              "nodeTxId": "f678722820b8aa8136bf6f41228d8e6f4983c7747f14b014a61df2dd2d1a41fb",
              "nodeAddress": "1J7e9Y6jTPnDoCkfFsmvzxketgDCf8Km7X",
              "nodePublicKey": "NULL",
              "parentTxId": "e24fd7d979e73528707ed8af267e5d453bb8cf65e5cb51a04234347e9d27c539",
              "parentAddress": "196iPAgmCyFRtt4MsdKvtcKZDVRpMdKFMc",
              "parentPublicKey": "NULL",
              "outputIndex": 0,
              "blockHeight": 631827,
              "timestamp": 1587633554116,
              "isSelf": false,
              "children": [
                {
                  "nodeTxId": "487aa4deecaa5eabd24d7dfb97ded646e71503b26ac9100ff411822459b28daa",
                  "nodeAddress": "12cLrusqwuq6Waryp2u5bmvZ6jskYAnb2W",
                  "nodePublicKey": "NULL",
                  "parentTxId": "f678722820b8aa8136bf6f41228d8e6f4983c7747f14b014a61df2dd2d1a41fb",
                  "parentAddress": "1J7e9Y6jTPnDoCkfFsmvzxketgDCf8Km7X",
                  "parentPublicKey": "NULL",
                  "outputIndex": 0,
                  "blockHeight": 631827,
                  "timestamp": 1587633554120,
                  "isSelf": false,
                  "children": null
                }
              ]
            }
          ]
        }
      ]
    }
  },
  "code": 200,
  "msg": "success",
  "time": 1590031505103,
  "error": "null"
}
```

-------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------

#### 3.2.5 根据address获取节点 `/api/v1/metanet/getMetaNodeByAddress/<address>` 

	请求协议：HTTP GET
	
	功能简介：根据address获取节点

************************************************ 请求参数 ************************************************

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| address          | string 	 | 	否           |	    			    |     txId           |

************************************************ 响应参数 ************************************************

***data***

|	参数名称     |	类型	 |	是否可空     |	长度限制			|	描述				            |
|----------------|-----------|---------------|----------------------|-----------------------------------|
| nodeTxId          | int64 	 | 	否           |	    			    | 节点txId              |
| nodeAddress       | string 	 | 	否      	 |	    			    | 节点地址		        |
| nodePublicKey     | string 	 | 	否      	 |	    			    | 节点公钥			    |
| parentTxId        | string 	 | 	否      	 |	    			    | 父节点txId			|
| parentAddress     | string 	 | 	否      	 |	    			    | 父节点地址			|
| parentPublicKey   | string 	 | 	否      	 |	    			    | 父节点公钥			|
| outputIndex       | int64 	 | 	否      	 |	    			    | 所在索引			    |
| blockHeight       | int64 	 | 	否      	 |	    			    | 块高			        |
| timestamp         | int64 	 | 	否      	 |	    			    | 时间戳			    |

************************************************ 请求响应实例 ************************************************	

```json
api请求数据: 
    http://test.showmoney.app/metaShow/api/v1/metanet/getMetaNodeByAddress/1GimPAbPAkmexbbdWqe9fQCQpgZdGNdjy7
    
响应数据：
{
  "result": [
    {
      "nodeTxId": "c37ee0eef4a98a192c42f28d8c66d3b10bd07a4c84d6a50445c9c9674b1179ed",
      "nodeAddress": "1GimPAbPAkmexbbdWqe9fQCQpgZdGNdjy7",
      "nodePublicKey": "NULL",
      "parentTxId": "8e9b396eb52752c95cfd45b86f9aa90e07e804ac38ff7f7f87669b0af2f06c86",
      "parentAddress": "NULL",
      "parentPublicKey": "NULL",
      "outputIndex": 0,
      "blockHeight": 631827,
      "rootTxId": "",
      "rootAddress": "",
      "rootPublicKey": "",
      "timestamp": 1588043791083
    },
    {
      "nodeTxId": "a5c05146de8fa49d8641cf34ae556c982048cd74a22731285dd744a48b5ed400",
      "nodeAddress": "1GimPAbPAkmexbbdWqe9fQCQpgZdGNdjy7",
      "nodePublicKey": "021a50ef584fa34b6d4067cd8457d38e8e20c9550b0cdc4fd7f00b2d67177128d6",
      "parentTxId": "57fab4aab7af94f7ed885cfc32ff6b15a4d90d400dea652f85390b4bec7b1051",
      "parentAddress": "NULL",
      "parentPublicKey": "NULL",
      "outputIndex": 0,
      "blockHeight": 632379,
      "rootTxId": "",
      "rootAddress": "",
      "rootPublicKey": "",
      "timestamp": 1588044715641
    }
  ],
  "code": 200,
  "msg": "success",
  "time": 1588254263493,
  "error": "null"
}
```

-------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------
