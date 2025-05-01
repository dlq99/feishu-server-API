## 获取OpenAPI审计日志数据

该接口用于获取OpenAPI审计日志数据

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/security_and_compliance/v1/openapi_logs/list_data` |
| HTTP Method | POST |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom |
| 权限要求 | 查看 OpenAPI 审计日志 |
| 权限要求 | security_and_compliance:audit_log.openapi_log:readonly |

### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| api_keys | undefined[] | 否 | 飞书开放平台定义的API，参考：[API列表](https://open.feishu.cn/document/server-docs/api-call-guide/server-api-list) <br> **示例**:  <br> **数据校验规则**:<br>最大长度: 100 |
| start_time | integer | 否 | 以秒为单位的起始时间戳 <br> **示例**: 1610613336  |
| end_time | integer | 否 | 以秒为单位的终止时间戳 <br> **示例**: 1610613336  |
| app_id | string | 否 | 调用OpenAPI的应用唯一标识，可以前往 [开发者后台](https://open.feishu.cn/app) > 应用详情页 > 凭证与基础信息中获取 app_id <br> **示例**: cli_xxx  |
| page_size | integer | 否 | 分页大小 <br> **示例**: 20  |
| page_token | string | 否 | 分页标记，第一次请求不填，表示从头开始遍历；分页查询结果还有更多项时会同时返回新的 page_token，下次遍历可采用该 page_token 获取查询结果 <br> **示例**: xxx  |

**请求体示例**:

```json
{
    "api_keys": [
        "POST/open-apis/authen/v1/access_token"
    ],
    "start_time": 1610613336,
    "end_time": 1610613336,
    "app_id": "cli_xxx",
    "page_size": 20,
    "page_token": "xxx"
}
```

### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "items": [
            {
                "id": "10000",
                "api_key": "POST/open-apis/demo/v1/example",
                "event_time": 1610613336,
                "app_id": "cli_xxx",
                "ip": "192.123.12.1",
                "log_detail": {
                    "path": "/open-apis/demo/v1/example",
                    "method": "POST",
                    "query_param": "{}",
                    "payload": "{\"param1\": \"val1\", \"param2\": \"val2\"}",
                    "status_code": 0,
                    "response": "{\"code\": 0, \"msg\": \"ok\"}"
                }
            }
        ],
        "page_token": "xxxx",
        "has_more": false
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 500 | 1780001 | Internal Server Error | 请重试，若仍有异常请联系开放平台技术支持 |
| 400 | 1780103 | Request Param Error | 参照文档说明检查输入参数 |

### 调用示例

#### C#-restsharp

```csharp
var client = new RestClient("https://open.feishu.cn/open-apis/security_and_compliance/v1/openapi_logs/list_data");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"api_keys\":[\"POST/open-apis/authen/v1/access_token\"],\"app_id\":\"cli_xxx\",\"end_time\":1610613336,\"page_size\":20,\"page_token\":\"xxx\",\"start_time\":1610613336}";
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
    "api_keys": [
        "POST/open-apis/authen/v1/access_token"
    ],
    "start_time": 1610613336,
    "end_time": 1610613336,
    "app_id": "cli_xxx",
    "page_size": 20,
    "page_token": "xxx"
}';
$request = new Request('POST', 'https://open.feishu.cn/open-apis/security_and_compliance/v1/openapi_logs/list_data', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X POST 'https://open.feishu.cn/open-apis/security_and_compliance/v1/openapi_logs/list_data' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"api_keys": [
		"POST/open-apis/authen/v1/access_token"
	],
	"app_id": "cli_xxx",
	"end_time": 1610613336,
	"page_size": 20,
	"page_token": "xxx",
	"start_time": 1610613336
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
	"github.com/larksuite/oapi-sdk-go/v3/service/security_and_compliance/v1"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larksecurity_and_compliance.NewListDataOpenapiLogReqBuilder().
		ListOpenapiLogRequest(larksecurity_and_compliance.NewListOpenapiLogRequestBuilder().
			ApiKeys([]string{`POST/open-apis/authen/v1/access_token`}).
			StartTime(1610613336).
			EndTime(1610613336).
			AppId(`cli_xxx`).
			PageSize(20).
			PageToken(`xxx`).
			Build()).
		Build()

	// 发起请求
	resp, err := client.SecurityAndCompliance.V1.OpenapiLog.ListData(context.Background(), req)

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
from lark_oapi.api.security_and_compliance.v1 import *


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
    request: ListDataOpenapiLogRequest = ListDataOpenapiLogRequest.builder() \
        .request_body(ListOpenapiLogRequest.builder()
            .api_keys(["POST/open-apis/authen/v1/access_token"])
            .start_time(1610613336)
            .end_time(1610613336)
            .app_id("cli_xxx")
            .page_size(20)
            .page_token("xxx")
            .build()) \
        .build()

    # 发起请求
    response: ListDataOpenapiLogResponse = client.security_and_compliance.v1.openapi_log.list_data(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.security_and_compliance.v1.openapi_log.list_data failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

#### Java SDK

```java
package com.lark.oapi.sample.apiall.security_and_compliancev1;
import com.google.gson.JsonParser;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.security_and_compliance.v1.model.*;
import java.util.HashMap;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class ListDataOpenapiLogSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      ListDataOpenapiLogReq req = ListDataOpenapiLogReq.newBuilder()
             .listOpenapiLogRequest(ListOpenapiLogRequest.newBuilder()
                 .apiKeys(new String[]{"POST/open-apis/authen/v1/access_token"})
                 .startTime(1610613336)
                 .endTime(1610613336)
                 .appId("cli_xxx")
                 .pageSize(20)
                 .pageToken("xxx")
                  .build())
             .build();

      // 发起请求
      ListDataOpenapiLogResp resp = client.securityAndCompliance().v1().openapiLog().listData(req);

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

client.securityAndCompliance.v1.openapiLog.listData({
        data: {
                api_keys:['POST/open-apis/authen/v1/access_token'],
                start_time:1610613336,
                end_time:1610613336,
                app_id:'cli_xxx',
                page_size:20,
                page_token:'xxx',
        },
},
    lark.withTenantToken("t-7f1b******8e560")
).then(res => {
    console.log(res);
}).catch(e => {
    console.error(JSON.stringify(e.response.data, null, 4));
});

```

