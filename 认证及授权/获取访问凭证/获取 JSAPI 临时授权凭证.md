# 获取 JSAPI 临时调用凭证

该接口用于返回调用 JSAPI 临时调用凭证，使用该凭证调用 JSAPI 时，请求不会被拦截。

## 使用说明

- 该接口适用于网页应用鉴权场景，详情参见鉴权调用 JSAPI。
- 获取 jsapi_ticket 的 API 调用次数非常有限，频繁刷新 jsapi_ticket 会导致 API 调用受限，影响自身业务。因此建议你在自己的服务全局缓存 jsapi_ticket。
- 获取 jsapi_ticket 后请结合返回的有效时间参数（expire_in），设置定时获取 jsapi_ticket 的逻辑，避免因凭证过期导致的业务异常。

## 请求
| 基本 |  |
| --- | --- |
| https://open.feishu.cn/open-apis/jssdk/ticket/get |
| POST |



### 请求头
| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| Authorization | string | 是 | `tenant_access_token`<br> <br>值格式："Bearer `access_token`"<br><br>示例值："Bearer t-7f1bcd13fc57d46bac21793a18e560"<br> <br> 了解更多：获取与使用access_token |
| Content-Type | string | 是 | 固定值："application/json; charset=utf-8" |



## 响应

### 响应体

| 参数         | 数据类型           | 说明      |
| --------- | ---------------  | -------  |
|code|int|错误码|
|msg|string|错误说明|
|data|object|业务数据|
|∟ticket|string|jsapi_ticket，调用 JSAPI 的临时票据||
|∟expire_in|int|ticket 的有效时间（单位：秒）|

### 响应体示例
  
```json
{
    "code": 0,
    "msg": "ok",
    "data": {
        "expire_in": 7200,
        "ticket": "0560604568baf296731aa37f0c8ebe3e049c19d7"
    }
}
```

### 错误码

具体可参考：服务端错误码说明