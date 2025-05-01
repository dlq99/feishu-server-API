# 调用服务端 API

本文档介绍如何通过 Go SDK，自行构建 API Client、构造 API 请求、最终成功调用服务端 API。你可前往[ API 调试台](https://open.feishu.cn/api-explorer?from=op_doc)，直接获取指定服务端 API 相关示例代码，然后参考本文档了解调用 API 的全面流程。

![](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/c1775342e5e95b326d5b41cd41f76c79_RfQtN36tq3.png?height=771&lazyload=true&maxWidth=750&width=1892)

## 步骤一：构建 API Client

通过 SDK 调用飞书开放接口之前，你需要先在代码中创建一个 API Client。该 API Client 支持指定当前使用的应用信息、日志级别、HTTP 请求超时时间等基本信息。以下为支持的配置项及其具体含义。

```go
var client = lark.NewClient("appID", "appSecret", // 默认配置为自建应用
    // lark.WithMarketplaceApp(), // 可设置为商店应用
    lark.WithLogLevel(larkcore.LogLevelDebug),
    lark.WithReqTimeout(3*time.Second),
    lark.WithEnableTokenCache(true),
    lark.WithHelpdeskCredential("id", "token"),
    lark.WithHttpClient(http.DefaultClient))
```

<md-dt-table>
<md-dt-thead>
<md-dt-tr>
<md-dt-th style="width: 20%;">配置选项
</md-dt-th>
<md-dt-th style="width: 20%;">配置方式
</md-dt-th>
<md-dt-th style="width: 10%;">是否必填
</md-dt-th>
<md-dt-th style="width: 30%;">描述
</md-dt-th>
</md-dt-tr>
</md-dt-thead>
<md-dt-tbody>
<md-dt-tr>
<md-dt-td>
<md-text type="field-name" >app_id 和 app_secret
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >`lark.NewClient("appID", "appSecret")`
</md-text>
</md-dt-td>
<md-dt-td>
是
</md-dt-td>
<md-dt-td>
应用凭证 App ID 和 App Secret。可在[开发者后台](https://open.feishu.cn/app) > 应用详情页 > **凭证与基础信息** > **应用凭证** 区域获取。![图片名称](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/f7f89950be7e57c2760a8b5b1f5e17c9_vnjP3lkiHz.png?height=524&lazyload=true&width=3594)
</md-dt-td>
</md-dt-tr>
<md-dt-tr>
<md-dt-td>
<md-text type="field-name" >AppType
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >`lark.WithMarketplaceApp()`
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
设置 App 类型为商店应用。如果你是 ISV 开发者，则必须设置该选项。关于商店应用的开发指南，可参见 [ISV（商店应用）开发指南](https://bytedance.feishu.cn/docx/DljadpCH3oMlnLxo1kpcS1vmnbg)。
</md-dt-td>
</md-dt-tr>
<md-dt-tr>
<md-dt-td>
<md-text type="field-name" >LogLevel
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >`lark.WithLogLevel(logLevel larkcore.LogLevel)`
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
设置 API Client 的日志输出级别，枚举值如下：
- LogLevelDebug
- LogLevelInfo（默认值）
- LogLevelWarn
- LogLevelError
</md-dt-td>
</md-dt-tr>
<md-dt-tr>
<md-dt-td>
<md-text type="field-name" >Logger
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >`lark.WithLogger(logger larkcore.Logger)`
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
设置API Client 的日志器，默认日志输出到标准输出。你可通过实现下面的 Logger 接口，来设置自定义的日志器。
```go
type Logger interface {
    Debug(context.Context, ...interface{})
    Info(context.Context, ...interface{})
    Warn(context.Context, ...interface{})
    Error(context.Context, ...interface{})
}
```
</md-dt-td>
</md-dt-tr>
<md-dt-tr>
<md-dt-td>
<md-text type="field-name" >LogReqAtDebug
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >`lark.WithLogReqAtDebug(printReqRespLog bool)`
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
设置是否开启 HTTP 请求参数和响应参数的日志打印开关。开启后，在 debug 模式下会打印 HTTP 请求和响应的 headers、body 等信息。

提示：在排查问题时开启该选项，有利于问题的排查。
</md-dt-td>
</md-dt-tr>
<md-dt-tr>
<md-dt-td>
<md-text type="field-name" >BaseUrl
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >`lark.WithOpenBaseUrl(baseUrl string)`
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
设置飞书域名，默认为飞书域名 FeishuBaseUrl。可用域名如下：
```go
// 飞书域名
var FeishuBaseUrl = "https://open.feishu.cn"

// Lark域名
var LarkBaseUrl = "https://open.larksuite.com"
```
</md-dt-td>
</md-dt-tr>
<md-dt-tr>
<md-dt-td>
<md-text type="field-name" >TokenCache
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >`lark.WithTokenCache(cache larkcore.Cache)`
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
设置 Token 缓存器，用于缓存 Token 和 appTIcket，默认实现为内存。如果你需要定制 Token 缓存器，则需实现如下 Cache 接口。
  
```go
type Cache interface {
    Set(ctx context.Context, key string, value string, expireTime time.Duration) error
  Get(ctx context.Context, key string) (string, error)
}
```
**注意**：对于商店应用的 ISV 开发者而言，如果需要 SDK 来缓存 appTicket，则需要实现该接口，以提供分布式缓存。
</md-dt-td>
</md-dt-tr>
<md-dt-tr>
<md-dt-td>
<md-text type="field-name" >EnableTokenCache
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >`lark.WithEnableTokenCache(enableTokenCache bool)`
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
设置是否开启 TenantAccessToken （应用访问凭证）的自动获取与缓存。

默认开启，如需关闭可设置为 false。
</md-dt-td>
</md-dt-tr>
<md-dt-tr>
<md-dt-td>
<md-text type="field-name" >HelpDeskId、HelpDeskToken
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >`lark.WithHelpdeskCredential(helpdeskID, helpdeskToken string)`
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
服务台的 ID 和 token。仅在调用服务台业务的 API 时需要配置。可在服务台管理后台](https://feishu.cn/helpdesk/admin)**设置中心** > **API 凭证** 处获取，详情参见 [服务台接入指南。**注意**：服务台的 ID、Token 只有服务台创建者可以查看到。

![图片名称](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/dcc3b0ac14729354c2bc4b44af26c4f9_pgEg9OZJW8.png?height=693&lazyload=true&width=1916)
</md-dt-td>
</md-dt-tr>
<md-dt-tr>
<md-dt-td>
<md-text type="field-name" >ReqTimeout
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >`lark.WithReqTimeout(time time.Duration)`
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
设置 SDK 内置的 Http Client 的请求超时时间。默认为 0 表示永不超时。
</md-dt-td>
</md-dt-tr>
<md-dt-tr>
<md-dt-td>
<md-text type="field-name" >HttpClient
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >`lark.WithHttpClient(httpClient larkcore.HttpClient)`
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
设置 Http Client，用于替换 SDK 提供的默认实现。你可通过实现下面的 HttpClient 接口来设置自定义的 HttpClient。
```go
type HttpClient interface {
  Do(*http.Request) (*http.Response, error)
}
```
</md-dt-td>
</md-dt-tr>
</md-dt-tbody>
</md-dt-table>

示例配置：
- 对于自建应用，使用以下代码创建 API Client。

    ```go
    var client = lark.NewClient("appID", "appSecret") // 默认配置为自建应用
    ```
    
- 对于商店应用，需在创建 API Client 时，使用 `lark.WithMarketplaceApp` 方法指定 AppType 为商店应用。了解更多可参考 [ISV（商店应用）开发指南](https://bytedance.feishu.cn/docx/DljadpCH3oMlnLxo1kpcS1vmnbg)。

  ```go
  var client = lark.NewClient("appID", "appSecret",lark.WithMarketplaceApp()) // 设置为商店应用
  ```

## 步骤二：构造 API 请求

在项目内创建 API Client 后，即可开始调用飞书开放平台接口。如下图示例，你可前往[ API 调试台](https://open.feishu.cn/api-explorer?from=op_doc)，直接获取指定服务端 API 相关示例代码。

![](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/0966179a94f58a48b933bb2e1f688617_hkFSCkZNsn.png?height=752&lazyload=true&maxWidth=750&width=1876)

SDK 使用 **client.** **业务域.** **版本.** **资源** **.方法名称** 来定位具体的 API 方法。以创建文档接口为例，HTTP URL 为 `https://open.feishu.cn/open-apis/docx/v1/documents`，其中 `docx` 为业务域，`v1` 为版本，`documents` 为资源，相应的创建方法为 `client.Docx.V1.Document.Create()`。

![](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/ee49322885bffb64b77fa2a7b3257b84_o5GLSFOUWR.png?height=676&lazyload=true&maxWidth=750&width=1670)

如下代码示例，你可通过 client 调用文档资源的 create 方法，创建一个文档。



> **📝 注意**
> 该示例需要你在开发者后台为应用开通[创建及编辑新版文档]或[创建新版文档]权限，否则接口将报 99991672 错误码。



```go
package main
import ( // 导入接口所属的业务资源包
        "context"
        "fmt"
        "github.com/larksuite/oapi-sdk-go/v3"
        "github.com/larksuite/oapi-sdk-go/v3/core"
        "github.com/larksuite/oapi-sdk-go/v3/service/docx/v1"
)
func main() {
        // 创建 API Client。你需在此传入你的应用的实际 App ID 和 App Secret
        client := lark.NewClient("appID", "appSecret")
        // 发起创建文档的请求
        resp, err := client.Docx.Document.Create(context.Background(), larkdocx.NewCreateDocumentReqBuilder().
                Body(larkdocx.NewCreateDocumentReqBodyBuilder().
                        FolderToken(""). // 文件夹 token，传空表示在根目录创建文档
                        Title("title"). // 文档标题
                        Build()).
                Build())
        //处理错误
        if err != nil {
           // 处理 err
           return
        }
        // 服务端错误处理
        if !resp.Success() {
           fmt.Println(resp.Code, resp.Msg, resp.LogId())
           return 
        }
        // 业务数据处理
        fmt.Println(larkcore.Prettify(resp.Data))
}
```
其他示例参考 GitHub 代码仓库中的[ im.go 示例](https://github.com/larksuite/oapi-sdk-go/blob/v3_main/sample/api/im/im.go)。

## （可选）步骤三：设置请求选项

在每次发起 API 调用时，你可以设置请求级别的相关参数，例如传递 userAccessToken（用户访问凭证）、自定义 headers 等。所有请求级别可设置的选项如下表所示。

| 配置选项 | 配置方式 | 描述 |
| --- | --- | --- |
| `Header` | `larkcore.WithHeaders(header http.Header)` | 设置自定义请求头。在发起请求时，这些请求头会被透传到飞书开放平台服务端。 |
| `UserAccessToken` | `larkcore.WithUserAccessToken(userAccessToken string)` | 设置用户 token，当你需要以用户身份发起 API 调用时，需要设置该选项的值。 |
| `TenantAccessToken` | `larkcore.WithTenantAccessToken(tenantAccessToken string)` | 设置企业或组织 token，当你自己维护企业或组织 token 时（即创建 client 时 EnableTokenCache 设置为 false），需通过该选项传递企业或组织 token。 |
| `TenantKey` | `larkcore.WithTenantKey(tenantKey string)` | 设置企业或组织 key，当你开发商店应用时，必须设置该选项。 |
| `RequestId` | `larkcore.WithRequestId(requestId string)` | 设置请求 ID，作为请求的唯一标识。该 ID 会被透传到飞书开放平台服务端。 |
| `NeedHelpDeskAuth` | `larkcore.WithNeedHelpDeskAuth()` | 设置添加服务台 helpdesk 的认证 header。 |



设置自定义请求头的示例代码如下所示。

```go
import (
        "context"
        "fmt"
        "net/http"
        "github.com/larksuite/oapi-sdk-go/v3"
        "github.com/larksuite/oapi-sdk-go/v3/core"
        "github.com/larksuite/oapi-sdk-go/v3/service/docx/v1"
)
func main() {
        // 创建 API Client。你需在此传入你的应用的实际 App ID 和 App Secret
        client := lark.NewClient("appID", "appSecret")
        // 设置自定义请求头
        header := make(http.Header)
        header.Add("k1", "v1")
        header.Add("k2", "v2")
        // 发起请求
        resp, err := client.Docx.Document.Create(context.Background(), larkdocx.NewCreateDocumentReqBuilder().
                Body(larkdocx.NewCreateDocumentReqBodyBuilder().
                        FolderToken("token").
                        Title("title").
                        Build(),
                ).
                Build(),
                larkcore.WithHeaders(header), // 设置自定义 headers
        )
        //处理错误
        if err != nil {
           // 处理 err
           return
        }
        // 服务端错误处理
        if !resp.Success() {
           fmt.Println(resp.Code, resp.Msg, resp.LogId())
           return
        }
        // 业务数据处理
        fmt.Println(larkcore.Prettify(resp.Data))
}
```

## 步骤四：运行代码

完成以上步骤后，即可运行代码调用创建文档 API。若请求成功，预计将返回以下数据。若失败，将返回错误码、错误信息和 Log ID，你可前往开发文档搜索解决方案。

```json
{
  Document: {
    DocumentId: "IPI4dqnbfoPxL3xhAEhcjXabcef",
    RevisionId: 1,
    Title: "title"
  }
}
```

## 常见问题

### 如何调用历史版本 API ？

服务端 API 中存在部分历史版本或未全量开放的接口，由于没有元数据信息，所以不能使用 SDK 内封装好的方法快速调用，此时你可以使用 SDK 提供的原生模式调用 API。以获取单个用户信息接口为例，调用示例如下所示：
```go
import (
        "context"
        "fmt"
        "github.com/larksuite/oapi-sdk-go/v3"
        "github.com/larksuite/oapi-sdk-go/v3/core"
        "net/http"
        "os"
)
func main() {
        // 创建 API Client。你需在此传入你的应用的实际 App ID 和 App Secret
        var appID, appSecret = os.Getenv("APP_ID"), os.Getenv("APP_SECRET")
        var cli = lark.NewClient(appID, appSecret)
        // 发起 API 请求
        resp, err := cli.Do(context.Background(),
                &larkcore.ApiReq{
                        HttpMethod:                http.MethodGet,
                        ApiPath:                   "https://open.feishu.cn/open-apis/contact/v3/users/:user_id",
                        Body:                      nil,
                        QueryParams:               larkcore.QueryParams{"user_id_type": []string{"open_id"}},
                        PathParams:                larkcore.PathParams{"user_id": "ou_c245b0a7dff2725cfa2fb104f8b48b9d"},
                        SupportedAccessTokenTypes: []larkcore.AccessTokenType{larkcore.AccessTokenTypeUser},
                },
        )
        // 错误处理
        if err != nil {
                fmt.Println(err)
                return
        }
        // 获取请求 ID
        fmt.Println(resp.LogId())
        // 处理请求结果
        fmt.Println(resp.StatusCode)      // http status code
        fmt.Println(resp.Header)          // http header
        fmt.Println(string(resp.RawBody)) // http body，二进制数据
}
```
了解更多 API 调用示例，参考 GitHub 代码仓库中的 [api.go 示例](https://github.com/larksuite/oapi-sdk-go/blob/v3_main/sample/callrawapi/api.go)。

### 如何快速获取接口对应的示例代码？

飞书开放平台提供了 API 调试台](https://open.feishu.cn/api-explorer)，通过该平台可以快速调试服务端 API，快速获取资源 ID 及生成多语言示例代码的能力，为您节省开发成本。例如，通过 API 调试台调用 [发送消息 接口，在调试台成功完成测试后，可通过 **示例代码** 页面查阅 Go SDK 对应的接口调用代码。

![](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/ca14b04adb4859f7971208d4f0128f08_dVOBqCWlWq.png?height=768&lazyload=true&maxWidth=750&width=1266)

### 如何准确选择 API 方法？

使用 API Client 调用 API 时，对应的方法建议你借助 API 调试台](https://open.feishu.cn/api-explorer/)获取，可通过指定接口的地址栏参数拼接方法，也可以直接参考接口提供的示例代码。以[通过手机号或邮箱获取用户 ID接口为例，获取方式如下图所示。

![](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/5b42cd293c1e26079d8ec616349f25b1_uVFNrtWSTM.png?height=1684&lazyload=true&maxWidth=750&width=2882)