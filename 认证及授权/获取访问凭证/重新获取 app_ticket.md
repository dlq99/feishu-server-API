# 重新获取 app_ticket

开放平台每隔 1 小时会向应用推送 app_ticket 事件，事件体内包含了 app_ticket。应用也可以主动调用此接口，触发开放平台即时推送 app_ticket 事件。了解事件信息可参见app_ticket 事件。

<md-alert type="error">

</md-alert>


<md-alert type="warn">

</md-alert>


<md-alert type="tip">

</md-alert>




## 请求
| 基本 |  |
| --- | --- |
| https://open.feishu.cn/open-apis/auth/v3/app_ticket/resend |
| POST |
|  |
| 无 |


### 请求头
| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| Content-Type | string | 是 | 固定值："application/json; charset=utf-8" |





### 请求体

| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| app_id | string | 是 | 应用唯一标识，创建应用后获得。有关`app_id` 的详细介绍。请参考通用参数介绍<br> <br>示例值： "cli_slkdjalasdkjasd" |
| app_secret | string | 是 | 应用秘钥，创建应用后获得。有关 `app_secret` 的详细介绍，请参考通用参数介绍<br> <br>示例值： "dskLLdkasdjlasdKK" |





### 请求体示例

```json
{
    "app_id": "cli_slkdjalasdkjasd",
    "app_secret": "dskLLdkasdjlasdKK"
}
```



## 响应



### 响应体
| 名称 | 类型 | 描述 |
| --- | --- | --- |
| code | int | 错误码，非 0 表示失败 |
| msg | string | 错误描述 |





### 响应体示例

```json
{
    "code": 0,
    "msg": "success"
}
```

### 错误码
有关错误码的详细介绍，请参考通用错误码介绍。


