# 调用 API

为了让开发者可以便捷地调用 API，飞书开放平台提供了 Java SDK、Go SDK、Python SDK 和 Node SDK。有关 SDK 的详细介绍，可以参考服务端 SDK。本文介绍基本的 API 调用方法。

## 前提条件

- 完成创建应用、申请权限、获取访问凭证、设置 IP 白名单之后，才能调用服务端 API。
- 调用 API 时，需要将访问凭证放入请求 Header 中（`Authorization:Bearer <access token>`）。
- 调用服务端 API 时，需要使用 HTTPS 协议、UTF-8 编码。

## 调用示例

### 向企业内员工发消息

你可以调用发送消息接口完成向企业内员工发消息的操作，从接口文档中可以确定，调用该接口前，需要获取 `tenant_access_token`。

1.  参考 获取访问凭证 获取 `tenant_access_token`。
    
    获取凭证的请求示例如下，你需要将 *app_id* 和 *app_secret* 替换为实际值。

    ```bash
    curl -X POST 'https://open.feishu.cn/open-apis/auth/v3/tenant_access_token/internal/'
    -H 'Content-Type: application/json; charset=utf-8' 
    -d '{
    "app_id": "<app_id>",
    "app_secret": "<app_secret>"
	}'
    ```
    
2. 根据文档内的请求参数描述，调用发送消息接口。

	- 方式一：在调试台发起 API 调用
	
		![image.png](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/aa007bc867dc38d935cdcd335a037c06_smkGlGqsxN.png?height=332&lazyload=true&maxWidth=600&width=943)
	- 方式二：本地发送 curl 请求
	
		该 API 需要使用 POST 方式发起。
			
		![image.png](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/85be6f7b4a4611d41665b1120c1b1445_0TGCvluM2T.png?height=366&lazyload=true&maxWidth=600&width=730)
		
		示例如下，请将参数示例值替换为实际值。
    
		```bash
		curl -X POST 'https://open.feishu.cn/open-apis/im/v1/messages?receive_id_type=user_id'
		-H 'Authorization:Bearer <tenant_access_token>'
		-H 'content-type:application/json; charset=utf-8'
		-d '{
	        	"content": {
	                	"text": "Hello World"
	        	},
	        	"msg_type": "text",
 	       	"receive_id": "<user_id>"
		}'
		``` 
        
        - *receive_id_type* 作为查询参数。
		- *content* *、msg_type* 和 *receive_id* 作为请求的 Body 内容。
		- 请求所需的 `tenant_access_token` 和 Content-Type 放在 Header 中。
	

### 查询用户信息

你可以调用获取单个用户信息接口查询用户信息。从接口文档中可以确定，调用该接口前，需要获取 `tenant_access_token` 或 `user_access_token`，请根据需要获取的用户信息范围，选择合适的访问凭证。

1. 参考 获取访问凭证 获取 `tenant_access_token` 或 `user_access_token`。

2. 根据文档内的请求参数描述，调用获取单个用户信息接口。

	- 方式一：在调试台发起 API 调用
    
    	![](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/60edbe9c112de55e65427818eab3fa06_DE7dVr6hYb.png?height=151&lazyload=true&maxWidth=350&width=437)
    
	- 方式二：本地发送 curl 请求

     	从接口文档中可以看出，`user_id` 是该接口的路径参数，例如我们查询一个 `user_id` 为 `ou_c99c5f35d542efc7ee492afe11af19ef` 的用户信息，示例如下：
   
     	```bash
        curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users/ou_c99c5f35d542efc7ee492afe11af19ef?user_id_type=user_id' \
        -H 'Authorization: Bearer <tenant_access_token>' \
        -H 'Content-Type: application/json; charset=utf-8'
     	```
     
## 响应结果

绝大多数 API 的响应体结构包括 `code`、`msg`、`data` 三个部分：
- `code`：错误码。如果是成功响应，`code` 取值为 0。
- `msg` ：错误信息。
- `data`：API 的调用结果。`data` 在一些操作类 API 的返回中可能不存在。


> **📝 注意**
> - 请不要依据 `msg` 来判定一个请求是否失败。
> - 接收到失败响应后，你可以先查看 通用错误码说明，排查问题。如果依然不能解决问题，可以向飞书开放平台反馈响应头中的 `x-tt-logid` 值，以便我们协助定位问题。



成功响应示例：
```json
{
  "code": 0,
  "msg": "success",
  "data": {
    // 响应的具体数据内容
  }
}
```
失败响应示例：
```json
{
  "code": 40004,
  "msg": "no dept authority error"
}
```

## 错误响应说明

飞书开放平台 OpenAPI 错误信息模块包含 HTTP 状态码、业务状态码（code）、错误信息（msg）、错误排查信息（error）四个大类。

::: warning
由于在接口迭代的过程中，错误信息（msg）可能会随时发生变化，因此开发者需要避免在代码逻辑里依赖 msg，建议根据返回的业务状态码（code）判断一个请求是否失败。
:::

错误响应结构如下所示：

```json 
HTTP / 1.1 400 Bad Request // HTTP 状态码
{
    "code": 44004,
    // 业务状态码
    "msg": "{error msg}, {help}, {url}.",
    // 错误信息
    "error": {
        "message": "Refer to the documentation to fix the error: https://open.feishu.cn/document/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-obtain-openid",
        "field_violations": [
            {
                "field": "para_a",
                "value": "testvalue_a",
                "description": "test description_a"
            }
        ],
        "permission_violations": [
            {
                "scope": "lark.im.xxx",
                "url": "https://open.feishu.cn/apps/cli_xxxx/auth"
            }
        ],
        "helps": [
            {
                "url": "https://open.feishu.cn/app/cli_a61e4f821889d00c/auth?q=event:ip_list&op_from=openapi",
                "description": "Learn more about scopes and how to add them: [event:ip_list]"
            }
        ],
        "logid": "xxx",
        "troubleshooter": "排查建议查看（Troubleshooting suggestions）：https://open.feishu.cn/search?from=openapi&log_id=XXXX&code=XXX&method_id=XXX"
    }
}
``` 
        
:::html
<md-dt-table>
<md-dt-thead>
<md-dt-tr>
<md-dt-th style="width: 30%;">错误信息模块</md-dt-th>
<md-dt-th >描述</md-dt-th>
</md-dt-tr>
</md-dt-thead>
<md-dt-tbody>
<md-dt-tr level="0">
<md-dt-td>HTTP 状态码</md-dt-td>
<md-dt-td>用于进行错误分类，如客户端错误（4XX）、服务端错误（5XX）。</md-dt-td>
</md-dt-tr>
<md-dt-tr level="0">
<md-dt-td>业务状态码 (code)</md-dt-td>
<md-dt-td>代表具体的错误场景，如参数错误、鉴权错误。业务失败情况下，返回非 0 业务状态码，且 HTTP 状态码为 400 或 500 系列。</md-dt-td>
</md-dt-tr>
<md-dt-tr level="0">
<md-dt-td>错误信息 (msg)</md-dt-td>
<md-dt-td>错误码 code 关联的具体错误描述。**msg** 可能会优化和调整，因此不要依赖 **msg** 进行代码判断，建议依赖 **code** 进行请求失败的代码判断。</md-dt-td>
</md-dt-tr>
<md-dt-tr level="0">
<md-dt-td>错误排查信息 (error)</md-dt-td>
<md-dt-td>说明具体是哪个部分出现了问题，帮助开发者定位错误的原因，并提供建议的解决方案。</md-dt-td>
</md-dt-tr>
<md-dt-tr level="1">
<md-dt-td>message</md-dt-td>
<md-dt-td>提供当前错误场景的更多帮助信息，如错误参数内容。</md-dt-td>
</md-dt-tr>
<md-dt-tr level="1">
<md-dt-td>troubleshooter</md-dt-td>
<md-dt-td>该字段的值是一个链接，可以直接复制后用浏览器打开，页面中会给出错误原因分析和对应的解决方案。

        
 


> **📝 注意**
> 如果你是在独立的 API 调试台或 API 文档内嵌的调试台中进行调试调用，可以直接在下方获取智能助手的详细排查建议。
> 
>   
>   
>   </md-dt-td>
> </md-dt-tr>
> <md-dt-tr level="1">
> <md-dt-td>logid</md-dt-td>
> <md-dt-td>API 调用日志 ID，可以通过在开放平台官网上搜索 logid 字段，获取详细的错误原因和排查建议。
>   
>         
>     
> 你也可以登录[开发者后台](https://open.feishu.cn/app)并进入调用 API 的应用的详情页，在 **日志检索** > **服务端日志检索** 功能页过滤出对应的 API 调用日志数据。
>     
>     </md-dt-td>
> </md-dt-tr>
> <md-dt-tr level="1">
> <md-dt-td>field_violations</md-dt-td>
> <md-dt-td>代表参数错误，当请求不满足参数数据校验规则时，返回的错误信息会包含该参数。例如，某 int 类型请求参数要求传值在 1~10 之间，实际请求时传入了 11 则会报错并返回 field_violations。你的服务可依赖该参数进行代码处理。field_violation 为数组，数组内结构为 Object。结构示例如下：
> ```json
> {
>     "field_violations": [
>         {
>             "field": "para_a",
>             "value": "testvalue_a",
>             "description": "test description_a"
>         }
>     ]
> }
> ```
>   </md-dt-td>
> </md-dt-tr>
> <md-dt-tr level="2">
> <md-dt-td>field</md-dt-td>
> <md-dt-td>具体的错误参数</md-dt-td>
> </md-dt-tr>
> <md-dt-tr level="2">
> <md-dt-td>value</md-dt-td>
> <md-dt-td>错误参数的取值</md-dt-td>
> </md-dt-tr>
> <md-dt-tr level="2">
> <md-dt-td>description</md-dt-td>
> <md-dt-td>字段错误的描述</md-dt-td>
> </md-dt-tr>
> <md-dt-tr level="1">
> <md-dt-td>permission_violations</md-dt-td>
> <md-dt-td>代表权限错误，请求时如果应用开通的权限不满足 API 需要会报错并返回该参数。你的服务可依赖该参数进行代码处理。permission_violation 为数组，数组内结构为 Object。结构示例如下：
>   
> ```json
> {
>     "permission_violations": [
>         {
>             "scope": "lark.im.xxx",
>             "url": "https://open.feishu.cn/apps/cli_xxxx/auth"
>         }
>     ]
> }
> ```
>   
>   
>   
>   </md-dt-td>
> </md-dt-tr>
> <md-dt-tr level="2">
> <md-dt-td>scope</md-dt-td>
> <md-dt-td>需要开通的权限。</md-dt-td>
> </md-dt-tr>
> <md-dt-tr level="2">
> <md-dt-td>url</md-dt-td>
> <md-dt-td>对应的添加权限的地址。可以点击后直接前往开发者后台权限页面进行申请开通。</md-dt-td>
> </md-dt-tr>
> <md-dt-tr level="1">
> <md-dt-td>helps</md-dt-td>
> <md-dt-td>权限不足时返回该参数，你可以访问 URL 快速跳转到缺失权限的应用 API 权限页面开通权限。结构示例如下：
> ```json  
> {
>     "helps": [
>         {
>             "url": "https://open.feishu.cn/app/cli_a61e4f1234xxx/auth?q=event:ip_list&op_from=openapi",
>             "description": "Learn more about scopes and how to add them: [event:ip_list]"
>         }
>     ]
> }
> ```
>   
>   </md-dt-td>
> </md-dt-tr>
> <md-dt-tr level="2">
> <md-dt-td>url</md-dt-td>
> <md-dt-td>对应的添加权限的地址。可以点击后直接前往开发者后台权限页面进行申请开通。</md-dt-td>
> </md-dt-tr>
> <md-dt-tr level="2">
> <md-dt-td>description</md-dt-td>
> <md-dt-td>提供缺失的权限信息。</md-dt-td>
> </md-dt-tr>
> </md-dt-tbody>
> </md-dt-table>


        
## 相关教程

你也可参考以下教程快速体验如何调用服务端 API：
- [快速调用一个服务端 API（以发送
消息接口为例）](/ssl:ttdoc/uAjLw4CM/uMzNwEjLzcDMx4yM3ATM/how-to-call-a-server-side-api/introduction)
- 快速调用一个服务端 API（以创建多维表格为例）