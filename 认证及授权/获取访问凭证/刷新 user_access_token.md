# 刷新 user_access_token

OAuth 令牌接口，可用于刷新 <code>user_access_token</code> 以及获取新的 <code>refresh_token</code>。


- `user_access_token` 为用户访问凭证，使用该凭证可以以用户身份调用 OpenAPI，该凭证存在有效期，可通过 `refresh_token` 进行刷新。
- `refresh_token` 用于获取新的 `user_access_token`，且仅能使用一次。在获取新的 `user_access_token` 时会返回新的 `refresh_token`，原 `refresh_token` 立即失效。

- 首次获取 `refresh_token` 的方式参见获取 user_access_token。

<md-alert type="tip">
  本接口实现遵循 [RFC 6749 - The OAuth 2.0 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749) ，你可以使用[标准的 OAuth 客户端库](https://oauth.net/code/)进行接入（**推荐**）
</md-alert>


## 前置工作
### 开通 offline_access 权限
获取 `refresh_token` 需前往开放平台应用后台的**权限管理**模块开通 `offline_access` 权限，并在发起授权时在 `scope` 参数中声明该权限。

![开通 offline_access 权限.png](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/f8b75edae2c682ab98b6984170707a64_gYt5eNq84a.png?height=703&lazyload=true&width=1867)

在开通 `offline_access` 权限后，如需获取 `refresh_token`，具体的请求参数设置如下：
1. 首先在发起授权时，授权链接的`scope` 参数中必须拼接 `offline_access`，例如：
```
https://accounts.feishu.cn/open-apis/authen/v1/authorize?client_id=cli_a5d611352af9d00b&redirect_uri=https%3A%2F%2Fexample.com%2Fapi%2Foauth%2Fcallback&scope=bitable:app:readonly%20offline_access
```
2. 在获取 user_access_token时，
	+ 如果不需要缩减权限，即该接口的 `scope` 参数为空，则无需做其他操作，即可正常获得 `refresh_token`；
	+ 如果需要缩减权限，即该接口的 `scope` 参数不为空，
		+ 且需要获取 `refresh_token`，则此处的 `scope` 参数中需要拼接 `offline_access`；
		+ 如不需要获取 `refresh_token`，则无需特殊处理；
3. 在刷新 user_access_token时，同第二步的逻辑。

### 开启刷新 user_access_token 的安全设置
<md-alert type="tip">
- 如果你看不到此开关则无需关注，其默认处于开启状态。
- 完成配置后需要发布应用使配置生效。具体操作参见发布企业自建应用、发布商店应用。
</md-alert>


前往开放平台应用后台的**安全设置**模块，打开刷新 `user_access_token` 的开关。


![开启刷新 user_access_token 的安全设置.png](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/194824525c33e70cd796579744571c2d_WbBjYQW3zR.png?height=796&lazyload=true&width=1907)

## 请求

<md-alert type="warn">
  为了避免刷新 `user_access_token` 的行为被滥用，在用户授权应用 365 天后，应用必须通过用户重新授权的方式来获取 `user_access_token` 与 `refresh_token`。如果 `refresh_token` 到期后继续刷新`user_access_token`将报错（错误码为 20037），可参考以下[错误码描述信息](#错误码)进行处理。
</md-alert>


<md-alert type="warn">
  刷新后请更新本地 `user_access_token` 和 `refresh_token`，原令牌将无法再使用（`user_access_token` 会有一分钟的豁免时间以供应用完成令牌轮转）。
</md-alert>


| 基本 |  |
| --- | --- |
| https://open.feishu.cn/open-apis/authen/v2/oauth/token |
| POST |
| 1000 次/分钟、50 次/秒 |
|  |
| 无 |
| `refresh_token` 以及 `refresh_token_expires_in` 字段仅在具备以下权限时返回：<br><br>offline_access |



### 请求头

| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| Content-Type | string | 是 | 请求体类型。<br><br>固定值：`application/json; charset=utf-8` |



### 请求体

| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |



### 请求体示例
```json
{
    "grant_type": "refresh_token",
    "client_id": "cli_a5ca35a685b0x26e",
    "client_secret": "baBqE5um9LbFGDy3X7LcfxQX1sqpXlwy",
    "refresh_token": "eyJhbGciOiJFUzI1NiIs**********XXOYOZz1mfgIYHwM8ZJA"
}
```
## 响应
响应体类型为 `application/json; charset=utf-8`。

### 响应体

| 名称 | 类型 | 描述 |
| --- | --- | --- |



### 响应体示例

成功响应示例：

```json
{
    "code": 0,
    "access_token": "eyJhbGciOiJFUzI1NiIs**********X6wrZHYKDxJkWwhdkrYg",
    "expires_in": 7200, // 非固定值，请务必根据响应体中返回的实际值来确定 access_token 的有效期
    "refresh_token": "eyJhbGciOiJFUzI1NiIs**********VXOYOZYZmfgIYHWM0ZJA",
    "refresh_token_expires_in": 604800, // 非固定值，请务必根据响应体中返回的实际值来确定 refresh_token 的有效期
    "scope": "auth:user.id:read offline_access task:task:read user_profile",
    "token_type": "Bearer"
}
```

失败响应示例：
```json
{
    "code": 20050,
    "error": "server_error",
    "error_description": "An unexpected server error occurred. Please retry your request."
}
```

### 错误码
| HTTP 状态码 | 错误码 | 描述 | 排查建议 |
| --- | --- | --- | --- |
| 400 | 20001 | The request is missing a required parameter. | 必要参数缺失，请检查请求时传入的参数是否有误 |
| 400 | 20002 | The client secret is invalid. | 应用认证失败，请检查提供的 `client_id` 与 `client_secret` 是否正确。获取方式参见 如何获取应用的 App ID。 |
| 400 | 20008 | The user does not exist. | 用户不存在，请检查发起授权的用户的当前状态 |
| 400 | 20009 | The specified app is not installed. | 租户未安装应用，请检查应用状态 |
| 400 | 20010 | The user does not have permission to use this app. | 用户无应用使用权限，请检查发起授权的用户是否仍具有应用使用权限 |
| 400 | 20024 | The provided authorization code or refresh token does not match the provided client ID. | 提供的 `refresh_token` 与 `client_id` 不匹配，请勿混用不同应用的凭证 |
| 400 | 20026 | The refresh token passed is invalid. Please check the value. | 请检查请求体中 `refresh_token` 字段的取值<br> <br>请注意本接口仅支持 v2 版本接口下发的 `refresh_token` |
| 400 | 20036 | The specified grant_type is not supported. | 无效的 `grant_type`，请检查请求体中 `grant_type` 字段的取值 |
| 400 | 20037 | The refresh token passed has expired. Please generate a new one. | `refresh_token` 已过期，请重新发起授权流程以获取新的 `refresh_token` |
| 400 | 20048 | The specified app does not exist. | 应用不存在，请检查应用状态 |
| 500 | 20050 | An unexpected server error occurred. Please retry your request. | 内部服务错误，请稍后重试，如果持续报错请联系[技术支持](https://applink.feishu.cn/TLJpeNdW) |
| 400 | 20063 | The request is malformed. Please check your request. | 请求体中缺少必要字段，请根据具体的错误信息补齐字段 |
| 400 | 20064 | The refresh token has been revoked. Please note that a refresh token can only be used once. | `refresh_token` 已被撤销，请重新发起授权流程以获取新的 `refresh_token` |
| 400 | 20066 | The user status is invalid. | 用户状态非法，请检查发起授权的用户的当前状态 |
| 400 | 20067 | The provided scope list contains duplicate scopes. Please ensure all scopes are unique. | 无效的 `scope` 列表，其中存在重复项，请确保传入的 `scope` 列表中没有重复项 |
| 400 | 20068 | The provided scope list contains scopes that are not permitted. Please ensure all scopes are allowed. | 无效的 `scope` 列表，其中存在用户未授权的权限。当前接口 `scope` 参数传入的权限必须是获取授权码时 `scope` 参数值的子集。<br> <br>例如，在获取授权码时，用户授权了权限 A、B，则当前接口 `scope` 可传入的值只有权限 A、B，若传入权限 C 则会返回当前错误码。 |
| 400 | 20069 | The specified app is not enabled. | 应用未启用，请检查应用状态 |
| 400 | 20070 | Multiple authentication methods were provided. Please only use one to proceed. | 请求使用了 `Basic Authentication`，同时也在请求体中传递了 `client_secret`，请仅使用一种认证方式 |
| 503 | 20072 | The server is temporarily unavailable. Please retry your request. | 服务暂不可用，请稍后重试 |
| 400 | 20073 | The refresh token has been used. Please note that a refresh token can only be used once. | 请重新发起授权流程以获取新的 `refresh_token` |
| 400 | 20074 | The specified app is not allowed to refresh token. | 请在应用管理后台检查是否开启了刷新 `user_access_token` 开关，注意发版后生效 |


