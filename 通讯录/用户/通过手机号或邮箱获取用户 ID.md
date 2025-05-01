## 通过手机号或邮箱获取用户 ID

调用该接口通过手机号或邮箱获取一个或多个用户的 ID （包括 user_id、open_id、union_id）与状态信息。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/contact/v3/users/batch_get_id` |
| HTTP Method | POST |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 获取用户 user ID <br> 以应用身份访问通讯录 <br> 读取通讯录 <br> 以应用身份读取通讯录 <br> 通过手机号或邮箱获取用户 ID <br> 获取用户受雇信息 |
| 权限要求 | contact:user.id:readonly |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| user_id_type | string | 否 | 用户 ID 类型 |
### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| emails | undefined[] | 否 | 要查询的用户邮箱，最多可传入 50 条。<br><br>**注意**：<br><br>- 不支持企业邮箱。<br>- emails 与 mobiles 两个参数相互独立，即每个用户邮箱会返回对应的用户信息，每个手机号也会返回对应的用户信息。<br>- 本接口返回的用户 ID 数量为 emails 数量与 mobiles 数量之和。<br><br>**默认值**：空 <br> **示例**: sync@a.com <br> **数据校验规则**:<br>最大长度: 50 |
| mobiles | undefined[] | 否 | 要查询的用户手机号，最多可传入 50 条。<br><br>**注意**：<br><br>- 非中国大陆地区的手机号需要添加以 “+” 开头的国家或地区代码。<br>- emails 与 mobiles 两个参数相互独立，即每个用户邮箱会返回对应的用户信息，每个手机号也会返回对应的用户信息。<br>- 本接口返回的用户 ID 数量为 emails 数量与 mobiles 数量之和。<br><br>**默认值**：空 <br> **示例**: 17839872039 <br> **数据校验规则**:<br>最大长度: 50 |
| include_resigned | boolean | 否 | 查询结果是否包含离职员工的用户信息。<br><br>**可选值有**：<br>- true：包含<br>- false：不包含 <br> **示例**: true  |

**请求体示例**:

```json
{
    "emails": [
"zhangsan@z.com","lisi@a.com"
    ],
    "mobiles": [
"13011111111","13022222222"
    ],
"include_resigned":true
}
```

### 响应

**响应示例**:

```json
{
	"code": 0,
	"msg": "success",
	"data": {
		"user_list": [{
				"user_id": "ou_979112345678741d29069abcdef01234",
				"email": "zhanxxxxx@a.com",
				"status": {
					"is_frozen": false,
					"is_resigned": false,
					"is_activated": true,
					"is_exited": false,
					"is_unjoin": false
				}
			}, {
				"user_id": "ou_919112245678741d29069abcdef02345",
				"email": "lisixxxx@a.com",
				"status": {
					"is_frozen": false,
					"is_resigned": false,
					"is_activated": true,
					"is_exited": false,
					"is_unjoin": false
				}
			},
			{
				"user_id": "ou_46a087654321a1dc920ffab8fedc3456",
				"mobile": "130xxxx1111",
				"status": {
					"is_frozen": false,
					"is_resigned": false,
					"is_activated": true,
					"is_exited": false,
					"is_unjoin": false
				}
			}, {
				"user_id": "ou_01b081675121a1dc920ffab97cdc4567",
				"mobile": "130xxxx2222",
				"status": {
					"is_frozen": false,
					"is_resigned": false,
					"is_activated": true,
					"is_exited": false,
					"is_unjoin": false
				}
			}
		]
	}
}
```

### 调用示例

#### Python SDK

```python
import json

import lark_oapi as lark
from lark_oapi.api.contact.v3 import *


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
    request: BatchGetIdUserRequest = BatchGetIdUserRequest.builder() \
        .user_id_type("user_id") \
        .request_body(BatchGetIdUserRequestBody.builder()
            .emails(["zhangsan@z.com", "lisi@a.com"])
            .mobiles(["13011111111", "13022222222"])
            .include_resigned(True)
            .build()) \
        .build()

    # 发起请求
    response: BatchGetIdUserResponse = client.contact.v3.user.batch_get_id(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.contact.v3.user.batch_get_id failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

#### Java SDK

```java
package com.lark.oapi.sample.apiall.contactv3;
import com.google.gson.JsonParser;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.contact.v3.model.*;
import java.util.HashMap;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class BatchGetIdUserSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      BatchGetIdUserReq req = BatchGetIdUserReq.newBuilder()
             .userIdType("user_id")
             .batchGetIdUserReqBody(BatchGetIdUserReqBody.newBuilder()
                 .emails(new String[]{"zhangsan@z.com","lisi@a.com"})
                 .mobiles(new String[]{"13011111111","13022222222"})
                 .includeResigned(true)
                  .build())
             .build();

      // 发起请求
      BatchGetIdUserResp resp = client.contact().v3().user().batchGetId(req);

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

client.contact.v3.user.batchGetId({
        params: {
                user_id_type:'user_id',
        },
        data: {
                emails:['zhangsan@z.com','lisi@a.com'],
                mobiles:['13011111111','13022222222'],
                include_resigned:true,
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
var client = new RestClient("https://open.feishu.cn/open-apis/contact/v3/users/batch_get_id?user_id_type=user_id");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"emails\":[\"zhangsan@z.com\",\"lisi@a.com\"],\"include_resigned\":true,\"mobiles\":[\"13011111111\",\"13022222222\"]}";
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
    "emails": [
"zhangsan@z.com","lisi@a.com"
    ],
    "mobiles": [
"13011111111","13022222222"
    ],
"include_resigned":true
}';
$request = new Request('POST', 'https://open.feishu.cn/open-apis/contact/v3/users/batch_get_id?user_id_type=user_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X POST 'https://open.feishu.cn/open-apis/contact/v3/users/batch_get_id?user_id_type=user_id' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"emails": [
		"zhangsan@z.com",
		"lisi@a.com"
	],
	"include_resigned": true,
	"mobiles": [
		"13011111111",
		"13022222222"
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
	"github.com/larksuite/oapi-sdk-go/v3/service/contact/v3"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkcontact.NewBatchGetIdUserReqBuilder().
		UserIdType(`user_id`).
		Body(larkcontact.NewBatchGetIdUserReqBodyBuilder().
			Emails([]string{`zhangsan@z.com`, `lisi@a.com`}).
			Mobiles([]string{`13011111111`, `13022222222`}).
			IncludeResigned(true).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Contact.V3.User.BatchGetId(context.Background(), req)

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

