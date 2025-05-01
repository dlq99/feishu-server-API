## 执行 OQL

在应用内执行 OQL 语句

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/apaas/v1/applications/:namespace/objects/oql_query` |
| HTTP Method | POST |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 创建、更新、删除对象记录数据 <br> 查看对象记录数据 |
| 权限要求 | app_engine:object.record:read <br> app_engine:object.record:write |

### 路径参数

| 参数名 | 类型 |  描述 |
| ------ | ---- | ---- |
| namespace | string | 应用命名空间 |

### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| query | string | 是 | 待执行的 OQL 语句 <br> **示例**: SELECT _id, _name FROM _user WHERE _type = $1 AND _accountStatus = $user_status LIMIT 10  |
| args | string | 否 | 用于指定 OQL 语句中匿名参数的具体值 <br> **示例**: [\"_employee\"]  |
| named_args | string | 否 | 用于指定 OQL 语句中具名参数的具体值 <br> **示例**: {\"user_status\" : \"_used\"}  |

**请求体示例**:

```json
{
    "query": "SELECT _id, _name FROM _user WHERE _type = $1 AND _accountStatus = $user_status LIMIT 10",
    "args": "[\"_employee\"]",
    "named_args": "{\"user_status\" : \"_used\"}"
}
```

### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "columns": [
            "_id"
        ],
        "rows": "[       {         \"_name\": \"Sample Text\",         \"_id\": 1234567890       }     ]"
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 400 | 2320001 | param is invalid | 请检查输入参数 |

### 调用示例

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

client.apaas.v1.applicationObject.oqlQuery({
        path: {
                namespace:'package_test__c',
        },
        data: {
                query:'SELECT _id, _name FROM _user WHERE _type = $1 AND _accountStatus = $user_status LIMIT 10',
                args:'["_employee"]',
                named_args:'{"user_status" : "_used"}',
        },
},
    lark.withTenantToken("t-7f1b******8e560")
).then(res => {
    console.log(res);
}).catch(e => {
    console.error(JSON.stringify(e.response.data, null, 4));
});

```

#### C#-restsharp

```csharp
var client = new RestClient("https://open.feishu.cn/open-apis/apaas/v1/applications/package_test__c/objects/oql_query");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"args\":\"[\\\"_employee\\\"]\",\"named_args\":\"{\\\"user_status\\\" : \\\"_used\\\"}\",\"query\":\"SELECT _id, _name FROM _user WHERE _type = $1 AND _accountStatus = $user_status LIMIT 10\"}";
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
    "query": "SELECT _id, _name FROM _user WHERE _type = $1 AND _accountStatus = $user_status LIMIT 10",
    "args": "[\"_employee\"]",
    "named_args": "{\"user_status\" : \"_used\"}"
}';
$request = new Request('POST', 'https://open.feishu.cn/open-apis/apaas/v1/applications/package_test__c/objects/oql_query', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X POST 'https://open.feishu.cn/open-apis/apaas/v1/applications/package_test__c/objects/oql_query' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"args": "[\"_employee\"]",
	"named_args": "{\"user_status\" : \"_used\"}",
	"query": "SELECT _id, _name FROM _user WHERE _type = $1 AND _accountStatus = $user_status LIMIT 10"
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
	"github.com/larksuite/oapi-sdk-go/v3/service/apaas/v1"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkapaas.NewOqlQueryApplicationObjectReqBuilder().
		Namespace(`package_test__c`).
		Body(larkapaas.NewOqlQueryApplicationObjectReqBodyBuilder().
			Query(`SELECT _id, _name FROM _user WHERE _type = $1 AND _accountStatus = $user_status LIMIT 10`).
			Args(`["_employee"]`).
			NamedArgs(`{"user_status" : "_used"}`).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Apaas.V1.ApplicationObject.OqlQuery(context.Background(), req)

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
from lark_oapi.api.apaas.v1 import *


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
    request: OqlQueryApplicationObjectRequest = OqlQueryApplicationObjectRequest.builder() \
        .namespace("package_test__c") \
        .request_body(OqlQueryApplicationObjectRequestBody.builder()
            .query("SELECT _id, _name FROM _user WHERE _type = $1 AND _accountStatus = $user_status LIMIT 10")
            .args("[\"_employee\"]")
            .named_args("{\"user_status\":\"_used\"}")
            .build()) \
        .build()

    # 发起请求
    response: OqlQueryApplicationObjectResponse = client.apaas.v1.application_object.oql_query(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.apaas.v1.application_object.oql_query failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

#### Java SDK

```java
package com.lark.oapi.sample.apiall.apaasv1;
import com.google.gson.JsonParser;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.apaas.v1.model.*;
import java.util.HashMap;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class OqlQueryApplicationObjectSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      OqlQueryApplicationObjectReq req = OqlQueryApplicationObjectReq.newBuilder()
             .namespace("package_test__c")
             .oqlQueryApplicationObjectReqBody(OqlQueryApplicationObjectReqBody.newBuilder()
                 .query("SELECT _id, _name FROM _user WHERE _type = $1 AND _accountStatus = $user_status LIMIT 10")
                 .args("[\"_employee\"]")
                 .namedArgs("{\"user_status\":\"_used\"}")
                  .build())
             .build();

      // 发起请求
      OqlQueryApplicationObjectResp resp = client.apaas().v1().applicationObject().oqlQuery(req);

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

