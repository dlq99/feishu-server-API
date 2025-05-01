# 自建应用获取 app_access_token

自建应用通过此接口获取`app_access_token`。{尝试一下}(url=/api/tools/api_explore/api_explore_config?project=auth&version=v3&resource=app_access_token&method=internal)





> **📝 注意**
> **说明：** `app_access_token` 的最大有效期是 2 小时。
> 
> - 如果在有效期小于 30 分钟的情况下，调用本接口，会返回一个新的 `app_access_token`，这会同时存在两个有效的 `app_access_token`。
> - 如果在有效期大于等于 30 分钟的情况下，调用本接口，会返回原有的 `app_access_token`。





## 请求
| 基本 |  |
| --- | --- |
| https://open.feishu.cn/open-apis/auth/v3/app_access_token/internal |
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
| code | int | 错误码，非 0 取值表示失败 |
| msg | string | 错误描述 |
| app_access_token | string | 应用访问凭证 |
| expire | int | `app_access_token` 的过期时间，单位为秒 |
| tenant_access_token | string | 租户访问凭证。了解不同的访问凭证，参见访问凭证介绍。 |





### 响应体示例

```json
{
    "app_access_token": "t-g1044ghJRUIJJ5ZPPZMOHKWZISL33E4QSS3abcef",
    "code": 0,
    "expire": 7200,
    "msg": "ok",
    "tenant_access_token": "t-g1044ghJRUIJJ5ZPPZMOHKWZISL33E4QSS3abcef"
}
```

### 错误码
有关错误码的详细介绍，请参考通用错误码介绍。

