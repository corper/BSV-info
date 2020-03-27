# bsv.info
BSV网络查询API。
该服务现处于Alpha测试阶段，仅供测试使用，请勿用于生产环境。

## 总体介绍
1. API URL: https://api.bsv.info
1. 应答消息格式: JSON

    | 参数 | 可选/必选 | 类型 | 说明 |
    | ---- | ---- | ---- | ---- |
    | error | 可选 | string | 当出错时会返回该字段，错误内容为字段的值 |
    | data | 可选 | object | 当没有错误时返回该字段，携带操作结果 |

## 接口说明
### UTXO

| 方法 | URI |
| ---- | ---- |
| GET | /utxo |


| 参数 | 可选/必选 | 取值范围 | 默认值 | 说明 |
| ---- | ---- | ---- | ---- | ---- |
| address | 与hash二选一 |  |  | 比特币地址 |
| hash | 与address二选一 | | | 对output script进行SHA256 hash之后的hex字符串 |
| limit | 可选 | 1 - 100 | 10 | 最多返回多少条结果 |
| offset | 可选 | 0 - 0xFFFFFFFF | 0 | 跳过多少条结果 |
| confirmed | 可选 | 0 - 1 | 1 | 是否查询已确认的UTXO |
| unconfirmed | 可选 | 0 - 1 | 0 | 是否查询未确认的UTXO |

#### 示例
##### 请求
https://api.bsv.info/utxo?address=1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa&offset=10&limit=2
##### 应答
```JSON
{
  "data":{
    "c": [
      {
        "v": 5500,
        "h": "02df529e8670aa4307965c7a4b7c15a8b2d5ad32e7f9c1e7c1874a6a59fbc0a5",
        "i": 1
      },
      {
        "v": 5500,
        "h": "0324b41c9e6a408c1305a74704a18cb9503b83da9e6a9fda17cd95f5051e1c85",
        "i": 0
      }
    ],
    "u": []
  }
}
```

| 字段 | 类型 | 可选/必选 | 说明 |
| ---- | ---- | ---- | ---- |
| c | Array | 可选 | Confirmed，已确认的UTXO列表 |
| u | Array | 可选 | Unconfirmed，未确认的UTXO列表，结构同已确认的UTXO列表 |
| c.v | Unsigned Integer | 必选 | Value，以satoshi为单位的比特币数量 | 
| c.h | String | 必选 | Hash，TXID |
| c.i | String | 必选 | Index， Output Index |

### TX查询

| 方法 | URI |
| ---- | ---- |
| GET | /tx |

| 参数 | 可选/必选 | 说明 |
| ---- | ---- | ---- |
| id | 必选 | TXID |

#### 示例
##### 请求
https://api.bsv.info/tx?id=4a5e1e4baab89f3a32518a88c31bc87f618f76673e2cc77ab2127b7afdeda33b
##### 应答
```JSON
{
  "data": {
    "hex": "01000000010000000000000000000000000000000000000000000000000000000000000000ffffffff4d04ffff001d0104455468652054696d65732030332f4a616e2f32303039204368616e63656c6c6f72206f6e206272696e6b206f66207365636f6e64206261696c6f757420666f722062616e6b73ffffffff0100f2052a01000000434104678afdb0fe5548271967f1a67130b7105cd6a828e03909a67962e0ea1f61deb649f6bc3f4cef38c4f35504e51ec112de5c384df7ba0b8d578a4c702b6bf11d5fac00000000"
  }
}
```

### output查询
| 方法 | URI |
| ---- | ---- |
| GET | /tx/output |

| 参数 | 可选/必选 | 说明 |
| ---- | ---- | ---- |
| id | 必选 | TXID |
| index | 必选 | output index |

#### 示例
##### 请求
https://api.bsv.info/tx/output?id=0defb1479e67fe9adc80708828a73f1476657ad3f3c89e563796b9f37a7897b1&index=1
##### 应答
```JSON
{
  "data":{
    "hex":"22020000000000001976a914666675d887a7ae09835af934096d9fcbbb70eed288ac"
  }
}
```

### input查询
| 方法 | URI |
| ---- | ---- |
| GET | /tx/input |

| 参数 | 可选/必选 | 说明 |
| ---- | ---- | ---- |
| id | 必选 | TXID |
| index | 必选 | input index |

#### 示例
##### 请求
https://api.bsv.info/tx/input?id=0defb1479e67fe9adc80708828a73f1476657ad3f3c89e563796b9f37a7897b1&index=0
##### 应答
```JSON
{
  "data":{
    "hex":"3f835c66077197054f04641bd1afe238a483a842fc18ee61884fcef4a63b6c9f020000006b483045022100e8cd72b69a06dfc0d356603ca0739b0f72a1af88c501cbff58b249e9837dc284022047658451c7e38b3e83e7bd47332d7561737ea6d666240ae4a0605711ac8e39ee41210295591ace9742ee4fe74403286d3a9416b2a18e76c3291816f1ca96c9eef5e8bfffffffff"
  }
}
```

### TX基本信息查询
| 方法 | URI |
| ---- | ---- |
| GET | /tx/desc |

| 参数 | 可选/必选 | 说明 |
| ---- | ---- | ---- |
| id | 必选 | TXID |

#### 示例
##### 请求
https://api.bsv.info/tx/desc?id=0defb1479e67fe9adc80708828a73f1476657ad3f3c89e563796b9f37a7897b1
##### 应答
```JSON
{
  "data": {
    "version": 1,
    "outputsNum": 3,
    "inputsNum": 1,
    "nLockTime": 0,
    "blockHash": "0000000000000000034eaca67a084df1de5b50ddebfef1c16e9fb5d90fdf6ab0",
    "indexInBlock": 6321
  }
}
```

| 字段 | 类型 | 可选/必选 | 说明 |
| ---- | ---- | ---- | ---- |
| version | Integer | 必选 | TX version |
| outputsNum | Unsigned Integer | 必选 | TX中outputs的数量 |
| inputsNum | Unsigned Integer | 必选 | TX中inputs的数量 | 
| nLockTime | Unsigned Integer | 必选 | TX的nLockTime |
| blockHash | String | 可选 | TX所在区块的hash |
| indexInBlock | Unsigned Integer | 可选 | TX在区块中的位置，0为起始位置 |


### TX广播

| 方法 | URI |
| ---- | ---- |
| POST | /tx/broadcast |

#### 示例
##### 请求
POST body:
```JSON
{
  "hex": "TX的HEX字符串"
}
```
##### 应答
```JSON
{
  "data": {
    "txid": "TX对应的TXID"
  }
}
```