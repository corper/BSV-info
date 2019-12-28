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
