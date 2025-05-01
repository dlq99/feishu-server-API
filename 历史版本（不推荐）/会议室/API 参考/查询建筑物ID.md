# 查询建筑物ID

该接口用于根据租户自定义建筑 ID 查询建筑 ID。
## 请求
| 基本 |  |
| --- | --- |
| https://open.feishu.cn/open-apis/meeting_room/building/batch_get_id?custom_building_ids=test01&custom_building_ids=test02 |
| GET |
|  |
| 获取会议室信息 |


### 请求头
| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| Authorization | string | 是 | `tenant_access_token`<br> <br>值格式："Bearer `access_token`"<br><br>示例值："Bearer t-7f1bcd13fc57d46bac21793a18e560"<br> <br> 了解更多：如何选择与获取 access token |
| Content-Type | string | 是 | 固定值："application/json; charset=utf-8" |



### 查询参数

| **参数**     | **参数类型** | **必须** | **说明**                                                     |
| ------------ | ------------ | -------- | ------------------------------------------------------------ |
| custom_building_ids | string       | 是       | 用于查询指定建筑物的租户自定义建筑ID |

## 响应

### 响应体

| **参数**     | **说明**                                             |
| ------------ | ---------------------------------------------------- |
| code         | 返回码，非 0 表示失败                                |
| msg          | 返回码的描述，"success" 表示成功，其他为错误提示信息 |
| data         | 返回业务信息                                         |
| ∟buildings   | 建筑列表                                             |
| &nbsp;&nbsp;&nbsp;∟building_id | 建筑物ID                                            |
| &nbsp;&nbsp;&nbsp;∟custom_building_id | 租户自定义建筑物ID              |


### 响应体示例

```json
{
    "code":0,
    "msg":"success",
    "data":{
        "buildings":[
            {
                "building_id":"omb_8ec170b937536a5d87c23b418b83f9bb",
                "custom_bulding_id":"test01"
            },
            {
                "building_id":"omb_38570e4f0fd9ecf15030d3cc8b388f3a",
                "custom_bulding_id":"test02"
            }
        ]
    }
}
```

### 错误码

具体可参考：服务端错误码说明
