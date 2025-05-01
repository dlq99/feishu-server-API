# 获取 user_access_token（小程序）

通过 login接口获取到登录凭证`code`后，开发者可以通过服务器发送请求的方式获取 session_key 和 用户凭证信息。



> **📝 注意**
> 本接口适用于 小程序登录 及小组件登录。





## 请求
| 基本 |  |
| --- | --- |
| https://open.feishu.cn/open-apis/mina/v2/tokenLoginValidate |
| POST |
|  |
| 无 |



### 请求头
| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| Authorization | string | 是 | `app_access_token`<br><br>值格式："Bearer `access_token`"<br><br>示例值："Bearer t-7f1bcd13fc57d46bac21793a18e560"<br><br>了解更多：获取与使用access_token |
| Content-Type | string | 是 | 固定值："application/json; charset=utf-8" |



### 请求体
参数 | 类型 | 必填 | 说明 
-- | -- | -- | -- 
code | string | 是 | 登录时获取的 code

### 请求体示例
```json
{
     "code": "2ef0bb04e272d274"
}
```

## 响应
### 响应体

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| code | int | 错误码，非 0 表示失败 |
| msg | string | 错误描述 |
| data | \- | \- |
| &emsp;∟&nbsp;open_id | string | 用户的Open ID，用于在同一个应用中对用户进行标识 |
| &emsp;∟&nbsp;employee_id | string | 用户的User ID，在职员工在企业内的唯一标识 <br><br>仅当开通以下权限后 返回该字段：<br>获取用户 user ID |
| &emsp;∟&nbsp;session_key | string | 会话密钥 |
| &emsp;∟&nbsp;tenant_key | string | 用户所在企业唯一标识 |
| &emsp;∟&nbsp;access_token | string | user_access_token，用户身份访问凭证 |
| &emsp;∟&nbsp;expires_in | int | user_access_token过期时间戳 |
| &emsp;∟&nbsp;refresh_token | string | 刷新用户 access_token 时使用的 token，过期时间为30天。刷新access_token 接口说明请查看文档 |



### 响应体示例
```json
{
    "code": 0,
    "msg": "success",
    "data": {
    	"open_id": "ou_194fcfc5e4b78db556a040ff5e42c0",
    	"employee_id":"6c486g",
    	"session_key": "e3aeb7df000c835365c630dac91bcf",
    	"tenant_key":"2c5914ac018f97",
    	"access_token":"u-tpwcnx2XzIcq8yHyJ6KL",
    	"expires_in":1565512680,
    	"refresh_token":"ur-W9dGvBJyVtwZmrwh0vBn"
    }
}
```

### 错误码
| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| --- | --- | --- | --- |
| 200 | 10202 | access token invalid | 检查 access_token 是否过期 |
| 200 | 10213 | code appid not match | 1. 获取code的应用与该接口的应用必须是同一个应用，请确认是否跨应用调用<br>2. code 仅能使用一次，请确认是否重复使用或者过期 |
| 200 | 10226 | invalid code | code不合法，请检查code是否合法或者过期 |
| 200 | 10228 | user to app has no visibility | 当前用户没有可见性 |






## 已知问题
返回的data中会包含一个union_id，该参数已废弃，与开放平台中常用的Union ID不是一个概念，请勿使用；如需要使用Union ID，可通过获取单个用户信息获取
:::html
