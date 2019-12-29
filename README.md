# bsv.info
BSV网络查询API

## 总体介绍
#### API URL
https://api.bsv.info

## 查询接口
### UTXO

| 方法 | URI |
| ---- | ---- |
| URI | /utxo |


| 参数 | 可选/必选 | 取值范围 | 默认值 | 说明 |
| ---- | ---- | ---- | ---- | ---- |
| address | 必选 |  |  | 比特币地址 |
| limit | 可选 | 1 - 100 | 10 | 最多返回多少条结果 |
| offset | 可选 | 0 - 0xFFFFFFFF | 0 | 跳过多少条结果 |
| confirmed | 可选 | 0 - 1 | 1 | 是否查询已确认的UTXO |
| unconfirmed | 可选 | 0 - 1 | 0 | 是否查询未确认的UTXO |

#### 示例
https://api.bsv.info/utxo?address=1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa&offset=10&limit=2
```JSON
  "c": [
    {
      "v": 5500,
      "e": {
        "h": "02df529e8670aa4307965c7a4b7c15a8b2d5ad32e7f9c1e7c1874a6a59fbc0a5",
        "i": 1
      }
    },
    {
      "v": 5500,
      "e": {
        "h": "0324b41c9e6a408c1305a74704a18cb9503b83da9e6a9fda17cd95f5051e1c85",
        "i": 0
      }
    }
  ],
  "u": []
}
```

| 字段 | 类型 | 可选/必选 | 说明 |
| ---- | ---- | ---- | ---- |
| c | Array | 必选 | 已确认的UTXO列表 |
| u | Array | 必选 | 未确认的UTXO列表，结构同已确认的UTXO列表 |
| c.v | Unsigned Integer | 必选 | 以satoshi为单位的比特币数量 | 
| c.e | Object | 必选 | Edge，用于定位UTXO所在的TX和Output Index |
| c.e.h | String | 必选 | Hash，TXID |
| c.e.i | String | 必选 | Index， Output Index |
