## 更新 URL 预览

该接口用于主动更新 [URL 预览](/ssl:ttdoc/uAjLw4CM/ukzMukzMukzM/development-link-preview/link-preview-development-guide)，调用后会重新触发一次客户端拉取，需要回调服务返回更新后的数据。

⚠️ 
 **注意**：更新链接预览时需要注意更新频率，如果更新时不指定用户，则可能会造成链接预览请求放大。例如，群聊中的链接预览，所有群成员均会尝试重新拉取预览请求。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/im/v2/url_previews/batch_update` |
| HTTP Method | POST |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 更新 URL 预览 |
| 权限要求 | im:url_preview.update |

### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| preview_tokens | undefined[] | 是 | URL 预览的 preview_tokens 列表。需要通过[拉取链接预览数据](/ssl:ttdoc/uAjLw4CM/ukzMukzMukzM/development-link-preview/pull-link-preview-data-callback-structure)回调获取 preview_tokens。<br><br>**注意**：单个 token 限制更新频率为 1次/5秒。 <br> **示例**:  <br> **数据校验规则**:<br>最大长度: 10最小长度: 1 |
| open_ids | undefined[] | 否 | 需要更新 URL 预览的用户 open_id。若不传，则默认更新 URL 预览所在会话的所有成员；若用户不在 URL 所在会话，则无法触发更新该用户对应的 URL 预览结果。获取方式参见[如何获取 Open ID](/ssl:ttdoc/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-obtain-openid)。 <br> **示例**:  <br> **数据校验规则**:<br>最大长度: 100最小长度: 0 |

**请求体示例**:

```json
{
    "preview_tokens": [
        "952te0c8-9ccf-463d-ad73-593f8f768a5c"
    ],
    "open_ids": [
        "ou_xxx"
    ]
}
```

### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "success",
    "data": {}
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 400 | 230001 | param is invalid | 参数错误，请根据接口返回的错误信息并参考文档检查输入参数。 |

### 调用示例

#### C#-restsharp

```csharp
var client = new RestClient("https://open.feishu.cn/open-apis/im/v2/url_previews/batch_update");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"open_ids\":[\"ou_xxx\"],\"preview_tokens\":[\"952te0c8-9ccf-463d-ad73-593f8f768a5c\"]}";
request.AddParameter("application/json", body,  ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
Console.WriteLine(response.Content);
```

#### Php-guzzle

```php
<?php
$client = new Client();
$headers = [
  'Authorization' => 'Bearer t-7f1b******8e560',
  'Content-Type' => 'application/json'
];
$body = '{
    "preview_tokens": [
        "952te0c8-9ccf-463d-ad73-593f8f768a5c"
    ],
    "open_ids": [
        "ou_xxx"
    ]
}';
$request = new Request('POST', 'https://open.feishu.cn/open-apis/im/v2/url_previews/batch_update', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X POST 'https://open.feishu.cn/open-apis/im/v2/url_previews/batch_update' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"open_ids": [
		"ou_xxx"
	],
	"preview_tokens": [
		"952te0c8-9ccf-463d-ad73-593f8f768a5c"
	]
}'
```

#### Golang SDK

```go
package main

import (
	"context"
	"fmt"
	"github.com/larksuite/oapi-sdk-go/v3"
	"github.com/larksuite/oapi-sdk-go/v3/core"
	"github.com/larksuite/oapi-sdk-go/v3/service/im/v2"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkim.NewBatchUpdateUrlPreviewReqBuilder().
		Body(larkim.NewBatchUpdateUrlPreviewReqBodyBuilder().
			PreviewTokens([]string{`952te0c8-9ccf-463d-ad73-593f8f768a5c`}).
			OpenIds([]string{`ou_xxx`}).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Im.V2.UrlPreview.BatchUpdate(context.Background(), req)

	// 处理错误
	if err != nil {
		fmt.Println(err)
		return
	}

	// 服务端错误处理
	if !resp.Success() {
		fmt.Printf("logId: %s, error response: \n%s", resp.RequestId(), larkcore.Prettify(resp.CodeError))
		return
	}

	// 业务处理
	fmt.Println(larkcore.Prettify(resp))
}

```

#### Python SDK

```python
import json

import lark_oapi as lark
from lark_oapi.api.im.v2 import *


# SDK 使用说明: https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/python--sdk/preparations-before-development
# 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
# 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
def main():
    # 创建client
    client = lark.Client.builder() \
        .app_id("YOUR_APP_ID") \
        .app_secret("YOUR_APP_SECRET") \
        .log_level(lark.LogLevel.DEBUG) \
        .build()

    # 构造请求对象
    request: BatchUpdateUrlPreviewRequest = BatchUpdateUrlPreviewRequest.builder() \
        .request_body(BatchUpdateUrlPreviewRequestBody.builder()
            .preview_tokens(["952te0c8-9ccf-463d-ad73-593f8f768a5c"])
            .open_ids(["ou_xxx"])
            .build()) \
        .build()

    # 发起请求
    response: BatchUpdateUrlPreviewResponse = client.im.v2.url_preview.batch_update(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.im.v2.url_preview.batch_update failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

#### Java SDK

```java
package com.lark.oapi.sample.apiall.imv2;
import com.google.gson.JsonParser;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.im.v2.model.*;
import java.util.HashMap;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class BatchUpdateUrlPreviewSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      BatchUpdateUrlPreviewReq req = BatchUpdateUrlPreviewReq.newBuilder()
             .batchUpdateUrlPreviewReqBody(BatchUpdateUrlPreviewReqBody.newBuilder()
                 .previewTokens(new String[]{"952te0c8-9ccf-463d-ad73-593f8f768a5c"})
                 .openIds(new String[]{"ou_xxx"})
                  .build())
             .build();

      // 发起请求
      BatchUpdateUrlPreviewResp resp = client.im().v2().urlPreview().batchUpdate(req);

       // 处理服务端错误
       if (!resp.success()) {
         System.out.println(String.format("code:%s,msg:%s,reqId:%s, resp:%s",
                    resp.getCode(), resp.getMsg(), resp.getRequestId(), Jsons.createGSON(true, false).toJson(JsonParser.parseString(new String(resp.getRawResponse().getBody(), StandardCharsets.UTF_8)))));
         return;
       }

       // 业务数据处理
         System.out.println(Jsons.DEFAULT.toJson(resp.getData()));
  }
}

```

#### Nodejs SDK

```javascript
// node-sdk使用说明：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/nodejs-sdk/preparation-before-development
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
const lark = require('@larksuiteoapi/node-sdk');

// 开发者复制该Demo后，需要修改Demo里面的"app id", "app secret"为自己应用的appId, appSecret
const client = new lark.Client({
    appId: 'app id',
    appSecret: 'app secret',
    // disableTokenCache为true时，SDK不会主动拉取并缓存token，这时需要在发起请求时，调用lark.withTenantToken("token")手动传递
    // disableTokenCache为false时，SDK会自动管理租户token的获取与刷新，无需使用lark.withTenantToken("token")手动传递token
    disableTokenCache: true
});

client.im.v2.urlPreview.batchUpdate({
        data: {
                preview_tokens:['952te0c8-9ccf-463d-ad73-593f8f768a5c'],
                open_ids:['ou_xxx'],
        },
},
    lark.withTenantToken("t-7f1b******8e560")
).then(res => {
    console.log(res);
}).catch(e => {
    console.error(JSON.stringify(e.response.data, null, 4));
});

```

