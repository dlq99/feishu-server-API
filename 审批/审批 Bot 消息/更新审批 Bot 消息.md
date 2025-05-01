# 更新审批 Bot 消息

调用发送审批 Bot 消息接口后，可根据审批 Bot 消息 ID 及审批相应的状态，更新审批 Bot 消息。例如，给审批人推送了审批待办消息，当审批人通过审批后，可以将之前推送的 Bot 消息更新为已审批。

## 使用限制

- 只能更新审批状态，以及审批同意或拒绝后的标题或者查看详情的文案。

- 只能更新模板为 1008「收到审批待办」的卡片。

- 只支持更新 30 天以内的审批 bot 消息。

## 请求

| 基本 |  |
| --- | --- |
| https://open.feishu.cn/open-apis/approval/v1/message/update |
| POST |
|  |
| 访问审批应用 |


### 请求头
| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| Authorization | string | 是 | `tenant_access_token`<br> <br>以应用身份调用 API，可读写的数据范围由应用自身的 数据权限范围 决定。参考 自建应用获取 tenant_access_token 或 商店应用获取 tenant_access_token。<br><br>值格式："Bearer `access_token`"<br><br>示例值："Bearer t-7f1bcd13fc57d46bac21793a181234" |
| Content-Type | string | 是 | 固定值："application/json; charset=utf-8" |



### 请求体

<md-dt-table>
<md-dt-thead>
<md-dt-tr>
<md-dt-th style="width: 20%;">参数</md-dt-th>
<md-dt-th style="width: 15%;">类型</md-dt-th>
<md-dt-th style="width: 15%;">必须</md-dt-th>
<md-dt-th style="width: 30%;">说明</md-dt-th>
</md-dt-tr>
</md-dt-thead>
<md-dt-tbody>
<md-dt-tr>
<md-dt-td>message_id</md-dt-td>
<md-dt-td>String</md-dt-td>
<md-dt-td>是</md-dt-td>
<md-dt-td>待更新的审批 Bot 消息 ID。调用发送审批 Bot 消息接口后，从返回结果中获取消息 ID。</md-dt-td>
</md-dt-tr>
<md-dt-tr>
<md-dt-td>status</md-dt-td>
<md-dt-td>string</md-dt-td>
<md-dt-td>是</md-dt-td>
<md-dt-td>状态类型，用于更新消息内第一个 `action` 的文字内容。可选值有：
- APPROVED：已同意
- REJECTED：已拒绝
- CANCELLED：已撤回
- FORWARDED：已转交
- ROLLBACK：已回退
- ADD：已加签
- DELETED：已删除
- PROCESSED：已处理
- CUSTOM：自定义按钮状态</md-dt-td>
</md-dt-tr>
<md-dt-tr>
<md-dt-td>status_name</md-dt-td>
<md-dt-td>String</md-dt-td>
<md-dt-td>否</md-dt-td>
<md-dt-td>当 status 取值 CUSTOM 时，可以自定义审批同意或拒绝后 title 内容。
      
**注意**:

- 这里传入的是国际化文案 Key（即 i18n_resources.texts 参数中的 Key），还需要在 i18n_resources.texts 参数中以 Key：Value 格式进行赋值。

- Key 需要以 `@i18n@` 开头。

**示例值**：@i18n@1</md-dt-td>
</md-dt-tr>
<md-dt-tr>
<md-dt-td>detail_action_name</md-dt-td>
<md-dt-td>String</md-dt-td>
<md-dt-td>否</md-dt-td>
<md-dt-td>当 status 取值 CUSTOM 时，可以自定义审批同意或拒绝后 **查看详情** 按钮名称。
   
**注意**:

- 这里传入的是国际化文案 Key（即 i18n_resources.texts 参数中的 Key），还需要在 i18n_resources.texts 参数中以 Key：Value 格式进行赋值。

- Key 需要以 `@i18n@` 开头。

**示例值**：@i18n@2</md-dt-td>
</md-dt-tr>
<md-dt-tr level="0">
<md-dt-td>i18n_resources</md-dt-td>
<md-dt-td>list</md-dt-td>
<md-dt-td>是</md-dt-td>
<md-dt-td>国际化文案。status_name、detail_action_name 参数设置了国际化文案 Key 后，需要通过 i18n_resources 设置 Key：value 关系为参数赋值。

例如，status_name取值为 @i18n@1，则需要在 i18n_resources.texts 中传入 `@i18n@1： 已废弃` 为参数赋值。
</md-dt-td>
</md-dt-tr>

<md-dt-tr level="1">
<md-dt-td>locale</md-dt-td>
<md-dt-td>string</md-dt-td>
<md-dt-td>是</md-dt-td>
<md-dt-td>语言。可选值有：

- zh-CN：中文
- en-US：英文
- ja-JP：日文

**示例值**：zh-CN
</md-dt-td>
</md-dt-tr>

<md-dt-tr level="1">
<md-dt-td>is_default</md-dt-td>
<md-dt-td>boolean</md-dt-td>
<md-dt-td>是</md-dt-td>
<md-dt-td>当前语言是否为默认语言。默认语言需要在 texts 中传入所有的 Key：Value，非默认语言如果缺失 Key，则会使用默认语言代替。

**示例值**：true</md-dt-td>
</md-dt-tr>

<md-dt-tr level="1">
<md-dt-td>texts</md-dt-td>
<md-dt-td>map</md-dt-td>
<md-dt-td>是</md-dt-td>
<md-dt-td>文案的 Key:Value。Key 需要以 `@i18n@` 开头，并按照各个参数的要求传入 Value。

**示例值**：

```
{
	"@i18n@1": "demotext1"，
	"@i18n@2": "demotext2"
}
```
</md-dt-td>
</md-dt-tr>
</md-dt-tbody>
</md-dt-table>



### 请求体示例

```json
{
    "message_id":"xxxx",
    "status":"CUSTOM",
    "status_name":"@i18n@1",
    "detail_action_name":"@i18n@2",
    "i18n_resources":[
        {
          "locale": "zh-CN",
          "texts" : {
              "@i18n@1": "已废弃",
              "@i18n@2": "已废弃按钮" 
            },
          "is_default": true
        }
    ]
}
```

## 响应

### 响应体

|参数|类型|说明|
|-|-|-|
|code|int|错误码，非 0 表示失败|
|msg|string|返回码的描述|
|data|map|返回业务信息|
|&emsp;∟message_id|string|消息 ID，用于继续更新审批 Bot 消息|

### 响应体示例

```json
{
    "code":0,
    "msg":"success",
    "data":{
        "message_id": "xxxx"
    }
}
```

### 错误码
具体可参考：服务端错误码说明