# Exchange 资源介绍

日历 API 提供了 Exchange 账户和飞书账户绑定、解绑以及状态查询的能力，你可以使用 API 将你的 Exchange 日历同步到飞书日历来使用。当 Exchange 账户绑定了飞书账户后，飞书账户会异步同步 Exchange 日历到飞书日历，同步期间你可以实时查询日历的同步状态。


##  字段说明

Exchange 绑定相关的 API 属性说明如下。

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| exchange_binding_id | string | 创建 Exchange 绑定关系时产生的 ID，是 admin 账户、exchange 账户、用户三元组的唯一标识 ID。你可以通过该 ID 查询绑定关系、日历同步状态，或者解除绑定关系。<br> <br>获取方式：调用将 Exchange 账户绑定到飞书账户接口时，从返回结果中获取。<br><br>示例值： "ZW1haWxfYWRtaW5fZXhhbXBsZUBvdXRsb29rLmNvbSBlbWFpbF9hY2NvdW50X2V4YW1wbGVAb3V0bG9vay5jb20=" |
| admin_account | string | Exchange 的 admin 账户。<br><br>示例值： "email_admin_example@outlook.com"<br> <br>字段权限要求：<br>获取用户邮箱信息 |
| exchange_account | string | 需绑定的 Exchange 账户。<br><br>示例值： "email_account_example@outlook.com"<br><br>字段权限要求：<br>获取用户邮箱信息 |
| user_id | string | 用户 ID，即 Exchange 账户绑定的飞书账户 ID。关于用户 ID 可参见用户相关的 ID 概念。<br> <br>示例值：ou_xxxxxxxxxxxxxxxxxx |
| status | string | Exchange 账户的同步状态。<br> <br>可选值：<br>- `doing`：日历正在同步<br>- `cal_done`：日历同步完成<br>- `timespan_done`：近期时间段同步完成<br>- `done`：日程同步完成<br>- `err`：同步错误<br> <br>示例值："doing" |



##  数据示例

```json
{
    "admin_account": "email_admin_example@outlook.com",
    "exchange_account": "email_account_example@outlook.com",
    "user_id": "ou_xxxxxxxxxxxxxxxxxx",
    "status": "doing",
    "exchange_binding_id": "ZW1haWxfYWRtaW5fZXhhbXBsZUBvdXRsb29rLmNvbSBlbWFpbF9hY2NvdW50X2V4YW1wbGVAb3V0bG9vay5jb20="
}
```