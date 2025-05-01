# 删除 Doc


该接口用于根据 docToken 删除对应的 Docs 文档。

<md-alert type="error">

为了更好地提升该接口的安全性，我们对其进行了升级，请尽快迁移至
  新版本>>

</md-alert>

<md-alert type="warn">

文档只能被文档所有者删除，文档被删除后将会放到回收站里
</md-alert>




> **📝 注意**
> 该接口不支持并发调用，且调用频率上限为5QPS



## 请求
| 基本 |  |
| --- | --- |
| https://open.feishu.cn/open-apis/drive/explorer/v2/file/docs/:docToken |
| DELETE |
|  |
| 查看、评论、编辑和管理云空间中所有文件<br>查看、评论、编辑和管理文档 |


### 请求头
| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| Authorization | string | 是 | `tenant_access_token`<br>或<br>`user_access_token`<br> <br>值格式："Bearer `access_token`"<br><br>示例值："Bearer u-7f1bcd13fc57d46bac21793a18e560"<br> <br> 了解更多：如何选择与获取 access token |



::: note
::: html
使用 `tenant_access_token` 前，请确保该应用是文档的所有者，否则会报无权限错误。
</md-td>
:::
<br>

### 路径参数
| 名称 | 类型 | 描述 |
| --- | --- | --- |
| docToken | string | doc 的 token，获取方式见 概述 |




## 响应
### 响应体
|参数|说明|
|--|--|
|id|doc 的 id「字符串类型」|
|result|删除结果|


### 响应体示例
```json
{
    "code":0,
    "msg":"success",
    "data":
    {
        "id":"id string",
        "result":true
    }
}
```
### 错误码

| 错误码 | 说明 | 排查建议 |
| --- | --- | --- |
| 91201 | FAILED | 处理失败，稍后重试。 |
| 91202 | PARAMERR | 参数错误，检查参数是否正确，如：`type`、`fileToken`、`dstFolderToken`。 |
| 91203 | NOTEXIST | 请检查请求参数是否正确，如：`type`跟`fileToken`是否匹配。 |
| 91204 | FORBIDDEN | 检查当前账户对文档、文件夹的权限。参考接入流程授权 |
| 91205 | DELETED | 来源文件已被删除，检查是否还存在。 |
| 91206 | OUT_OF_LIMIT | 超过限制。 |
| 91207 | DUPLICATE | 重复记录。 |
| 91208 | REVIEW | 内容审查不通过。 |



具体可参考：服务端错误码说明
