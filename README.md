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

### TX广播

| 方法 | URI |
| ---- | ---- |
| POST | /tx/broadcast |

#### 示例
##### 请求
POST body:
```JSON
{
  "hex": "tx的HEX字符串"
}
```
##### 应答
```JSON
{
  "txid": "tx对应的txid"
}
```