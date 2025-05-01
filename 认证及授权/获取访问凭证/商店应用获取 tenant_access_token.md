# 商店应用获取 tenant_access_token
商店应用通过此接口获取`tenant_access_token`。{尝试一下}(url=/api/tools/api_explore/api_explore_config?project=auth&version=v3&resource=tenant_access_token&method=create)



> **📝 注意**
> **说明** **：** `tenant_access_token` 的最大有效期是 2 小时。如果在有效期小于 30 分钟的情况下，调用本接口，会返回一个新的 `tenant_access_token`，这会同时存在两个有效的 `tenant_access_token`。





## 请求
| 基本 |  |
| --- | --- |
| https://open.feishu.cn/open-apis/auth/v3/tenant_access_token |
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
| app_access_token | string | 是 | 应用访问凭证，通过商店应用获取 app_access_token接口获取<br> <br>示例值： "a-32bd8551db2f081cbfd26293f27516390b9feb04" |
| tenant_key | string | 是 | 租户在飞书上的唯一标识，也可以理解为企业标识<br>可以通过如下方式获取：<br>- 企业开通应用时，开放平台推送给应用，具体可参考首次启用应用<br>- 用户登录到小程序、H5 应用或者浏览器应用时，在用户的身份信息中获取<br> <br>示例值："73658811060f175d" |





### 请求体示例

```json
{
    "app_access_token": "a-32bd8551db2f081cbfd26293f27516390b9feb04",
    "tenant_key": "73658811060f175d"
}
```



## 响应



### 响应体
| 名称 | 类型 | 描述 |
| --- | --- | --- |
| code | int | 错误码，非 0 取值表示失败 |
| msg | string | 错误描述 |
| tenant_access_token | string | 租户访问凭证 |
| expire | int | `tenant_access_token` 的过期时间，单位为秒 |





### 响应体示例

```json
{
    "code": 0,
    "msg": "success",
    "tenant_access_token": "t-caecc734c2e3328a62489fe0648c4b98779515d3",
    "expire": 7140
}
```

### 错误码

有关错误码的详细介绍，请参考通用错误码介绍。


