# 查询会议室ID

该接口用于根据租户自定义会议室ID查询会议室ID。

## 请求
| 基本 |  |
| --- | --- |
| https://open.feishu.cn/open-apis/meeting_room/room/batch_get_id?custom_room_ids=test01&custom_room_ids=test02 |
| GET |
|  |
| 获取会议室信息 |


### 请求头
| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| Authorization | string | 是 | `tenant_access_token`<br> <br>值格式："Bearer `access_token`"<br><br>示例值："Bearer t-7f1bcd13fc57d46bac21793a18e560"<br> <br> 了解更多：如何选择与获取 access token |
| Content-Type | string | 是 | 固定值："application/json; charset=utf-8" |



### 查询参数

| **参数** | **参数类型** | **必须** | **说明**                                                     |
| -------- | ------------ | -------- | ------------------------------------------------------------ |
| custom_room_ids | string       | 是       | 用于查询指定会议室的租户自定义会议室ID      |


## 响应

### 响应体

| **参数**       | **说明**                                                     |
| -------------- | ------------------------------------------------------------ |
| code           | 返回码，非 0 表示失败                                        |
| msg            | 返回码的描述，"success" 表示成功，其他为错误提示信息         |
| data           | 返回业务信息                                                 |
| ∟rooms         | 会议室列表                                                   |
| &nbsp;&nbsp;&nbsp;∟room_id       | 会议室 ID                                                    |
| &nbsp;&nbsp;&nbsp;∟custom_room_id   | 租户自定义会议室 ID                                          |

### 响应体示例

```json
{
    "code":0,
    "msg":"success",
    "data":{
        "rooms":[
            {
                "room_id":"omm_eada1d61a550955240c28757e7dec3af",
                "custom_room_id":"test01"
            },
            {
                "room_id":"omm_83d09ad4f6896e02029a6a075f71c9d1",
                "custom_room_id":"test02"
            }
        ]
    }
}
```

### 错误码

具体可参考：服务端错误码说明
