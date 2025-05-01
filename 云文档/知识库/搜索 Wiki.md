# 搜索 Wiki
搜索 Wiki，用户通过关键词查询 Wiki，只能查找自己可见的 wiki



> **📝 注意**
> **注：** Wiki 存在，但用户搜索不到并不一定是搜索有问题，可能是用户没有查看该 Wiki 的权限



## 请求
|基本| |
|:-----|:-----|
|HTTP URL|https://open.feishu.cn/open-apis/wiki/v1/nodes/search|
|HTTP Method|POST|
|HTTP Content-Type|application/json; charset=utf-8|
|凭证要求|user_access_token|
|权限要求|查看知识库|

### 查询参数
|属性名称|类型|必填|描述|
|:-----|:-----|:----|:-----|
|page_token|string|否|下一页的分页 token，首页不需要填写，根据返回的 token 获取下一页数据|
|page_size|int|否|本页返回数量的最大值 0 < page_size <= 50 默认 20|

### 请求体
|属性名称|类型|必填|描述|
|:-----|:-----|:----|:-----|
|query|string|是|搜索关键词|
|space_id|string|否|文档所属的知识空间ID，为空搜索全部知识空间|
|node_id|string|否|不为空搜索该节点及其所有子节点，为空搜索所有 wiki（使用 node_id 过滤必须传入 space_id）|

### 请求体示例
``` json
{
    "query": "搜索关键词",
    "space_id": "xxxxxxx",
    "node_id": "xxxx"
}
```

## 响应
### 响应体
|Name|Type|Description|
|:-----|:-----|:-----|
|code|int|错误码，非 0 表示失败|
|msg|string|错误描述|
|data|-|-|
|&nbsp; ∟items|list|wiki 信息数组|
|&nbsp; &nbsp; ∟node_id|string|wiki 节点的 token|
|&nbsp; &nbsp; ∟space_id|string|wiki 所属知识空间 Id|
|&nbsp; &nbsp; ∟obj_type|int|wiki 类型, 参考文档类型表|
|&nbsp; &nbsp; ∟obj_token|string|节点的真实文档的 token，如果要获取或编辑节点内容，需要使用此 token 调用对应的接口|
|&nbsp; &nbsp; ∟parent_id|string|暂未生效，一律返回空|
|&nbsp; &nbsp; ∟sort_id|int|该知识库文档的序号，从 1 开始计数|
|&nbsp; &nbsp; ∟title|string|wiki 标题|
|&nbsp; &nbsp; ∟url|string|wiki 的访问 url|
|&nbsp; &nbsp; ∟icon|string|wiki 对应图标的 url|
|&nbsp; ∟page_token|string|如果 has_more 为 true 则返回下一页的 token|
|&nbsp; ∟has_more|bool|是否还有下一页数据|

#### 文档类型表

|obj_type|说明|
|--|--|
|1|Doc|
|2|Sheet|
|3|Bitable|
|4|Mindnote|
|5|File|
|6|Slide|
|7|Wiki|
|8|Docx|
|9|Folder|
|10|Catalog|


### 响应体示例
``` json
{
  "code": 0,
  "data": {
    "has_more": false,
    "items": [
      {
        "node_id": "BAgPwq6lIi5Nykk0E5fcJeabcef",
        "obj_token": "AcnMdexrlokOShxe40Fc0Oabcef",
        "obj_type": 8,
        "parent_id": "",
        "sort_id": 1,
        "space_id": "7307457194084925443",
        "title": "欢迎使用知识库 / Welcome to Wiki",
        "url": "https://sample.feishu.cn/wiki/BAgPwq6lIi5Nykk0E5fcJeabcef"
      }
    ]
  },
  "msg": "success"
}
```

## 错误码
|HTTP 状态码|错误码|描述|排查建议|
|:-----|:-----|:-----|:-----|
|200|10001|invalid param|参数错误，参考文档检查输入参数|
|200|10002|network anomaly, please try again|后端服务异常或网络异常，可重新请求|