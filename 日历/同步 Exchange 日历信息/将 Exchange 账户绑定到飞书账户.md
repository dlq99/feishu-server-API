## 将 Exchange 账户绑定到飞书账户

调用该接口将 Exchange 账户绑定到飞书账户，进而支持 Exchange 日历的导入。

💡 
 当前身份需要是企业超级管理员。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/calendar/v4/exchange_bindings` |
| HTTP Method | POST |
| 支持的访问令牌 | user_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 获取用户邮箱信息 <br> 获取用户 user ID <br> 更新日历及日程信息 <br> 获取日历、日程及忙闲信息 <br> 创建 Exchange 绑定关系 |
| 权限要求 | calendar:calendar <br> calendar:calendar:readonly <br> calendar:exchange.bindings:create |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| user_id_type | string | 否 | 用户 ID 类型 |
### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| admin_account | string | 否 | Exchange 的 admin 账户。 <br> **示例**: email_admin_example@outlook.com <br> **数据校验规则**:<br>最大长度: 500最小长度: 1 |
| exchange_account | string | 否 | 需绑定的 Exchange 账户。 <br> **示例**: email_account_example@outlook.com <br> **数据校验规则**:<br>最大长度: 500最小长度: 1 |
| user_id | string | 否 | 用户 ID，即 Exchange 账户绑定的飞书账户 ID。关于用户 ID 可参见[用户相关的 ID 概念](/ssl:ttdoc/home/user-identity-introduction/introduction)。 <br> **示例**: ou_xxxxxxxxxxxxxxxxxx  |

**请求体示例**:

```json
{
    "admin_account": "email_admin_example@outlook.com",
    "exchange_account": "email_account_example@outlook.com",
    "user_id": "ou_xxxxxxxxxxxxxxxxxx"
}
```

### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "admin_account": "email_admin_example@outlook.com",
        "exchange_account": "email_account_example@outlook.com",
        "user_id": "ou_xxxxxxxxxxxxxxxxxx",
        "status": "doing",
        "exchange_binding_id": "ZW1haWxfYWRtaW5fZXhhbXBsZUBvdXRsb29rLmNvbSBlbWFpbF9hY2NvdW50X2V4YW1wbGVAb3V0bG9vay5jb20="
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 400 | 190002 | invalid parameters in request | 无效的请求参数。排查建议如下：<br><br>- 确认请求参数的字段名称、传参类型正确。<br>- 确认已经申请了相应资源的权限。<br>- 确认相应资源未被删除。 |
| 500 | 190003 | internal service error | 内部服务错误，请咨询[技术支持](https://applink.feishu.cn/TLJpeNdW)。 |
| 429 | 190004 | method rate limited | 方法频率限制。建议稍后再试，并适当减小请求 QPS。 |
| 429 | 190005 | app rate limited | 应用频率限制。建议稍后再试，并适当减小请求 QPS。 |
| 403 | 190006 | wrong unit for app tenant | 请求错误，检查应用 App ID 和 App Secret 是否正确。如仍无法解决请咨询[技术支持](https://applink.feishu.cn/TLJpeNdW)。 |
| 404 | 190007 | app bot_id not found | 应用的 bot_id 没有找到。你需要确保应用开启了[机器人能力](/ssl:ttdoc/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-enable-bot-ability)。如仍未解决请咨询[技术支持](https://applink.feishu.cn/TLJpeNdW)。 |
| 429 | 190010 | current operation rate limited | 当前操作被限流，原因一般为公用资源并发抢占失败。你可以适当降低当前操作频率，然后重试。 |
| 404 | 195100 | user is dismiss or not exist in the tenant | 当前身份或指定用户已经离职，或者不在该租户内。请检查并改为正确的身份来调用接口。 |
| 403 | 195101 | user is not supper administrator | 当前身份不是该租户的超级管理员。请检查并修改身份信息。 |
| 400 | 195102 | exchange_binding_id invalid | exchange_binding_id 无效。你需要检查并修改为正确的 ID。 |
| 404 | 195103 | exchange account binding is not found | exchange 账户的绑定关系没有找到。你需要检查输入参数是否填写正确。 |
| 403 | 195104 | current tenant not match | 当前租户与 admin 账户绑定的租户不匹配。你需要检查并修改为正确的参数值。 |
| 403 | 195105 | admin account binding failed | 管理后台绑定 admin 帐户失败。请在管理后台重新绑定 admin 账户后重试。 |
| 404 | 195106 | admin account is not found | admin 账户不存在。你需要检查并修改为正确的参数值。 |

### 调用示例

#### Php-guzzle

```php
<?php
$client = new Client();
$headers = [
  'Authorization' => 'Bearer t-7f1b******8e560',
  'Content-Type' => 'application/json'
];
$body = '{
    "admin_account": "email_admin_example@outlook.com",
    "exchange_account": "email_account_example@outlook.com",
    "user_id": "ou_xxxxxxxxxxxxxxxxxx"
}';
$request = new Request('POST', 'https://open.feishu.cn/open-apis/calendar/v4/exchange_bindings?user_id_type=open_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X POST 'https://open.feishu.cn/open-apis/calendar/v4/exchange_bindings?user_id_type=open_id' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"admin_account": "email_admin_example@outlook.com",
	"exchange_account": "email_account_example@outlook.com",
	"user_id": "ou_xxxxxxxxxxxxxxxxxx"
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
	"github.com/larksuite/oapi-sdk-go/v3/service/calendar/v4"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkcalendar.NewCreateExchangeBindingReqBuilder().
		UserIdType(`open_id`).
		ExchangeBinding(larkcalendar.NewExchangeBindingBuilder().
			AdminAccount(`email_admin_example@outlook.com`).
			ExchangeAccount(`email_account_example@outlook.com`).
			UserId(`ou_xxxxxxxxxxxxxxxxxx`).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Calendar.V4.ExchangeBinding.Create(context.Background(), req)

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
from lark_oapi.api.calendar.v4 import *


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
    request: CreateExchangeBindingRequest = CreateExchangeBindingRequest.builder() \
        .user_id_type("open_id") \
        .request_body(ExchangeBinding.builder()
            .admin_account("email_admin_example@outlook.com")
            .exchange_account("email_account_example@outlook.com")
            .user_id("ou_xxxxxxxxxxxxxxxxxx")
            .build()) \
        .build()

    # 发起请求
    response: CreateExchangeBindingResponse = client.calendar.v4.exchange_binding.create(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.calendar.v4.exchange_binding.create failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

#### Java SDK

```java
package com.lark.oapi.sample.apiall.calendarv4;
import com.google.gson.JsonParser;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.calendar.v4.model.*;
import java.util.HashMap;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class CreateExchangeBindingSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      CreateExchangeBindingReq req = CreateExchangeBindingReq.newBuilder()
             .userIdType("open_id")
             .exchangeBinding(ExchangeBinding.newBuilder()
                 .adminAccount("email_admin_example@outlook.com")
                 .exchangeAccount("email_account_example@outlook.com")
                 .userId("ou_xxxxxxxxxxxxxxxxxx")
                  .build())
             .build();

      // 发起请求
      CreateExchangeBindingResp resp = client.calendar().v4().exchangeBinding().create(req);

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

client.calendar.v4.exchangeBinding.create({
        params: {
                user_id_type:'open_id',
        },
        data: {
                admin_account:'email_admin_example@outlook.com',
                exchange_account:'email_account_example@outlook.com',
                user_id:'ou_xxxxxxxxxxxxxxxxxx',
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
var client = new RestClient("https://open.feishu.cn/open-apis/calendar/v4/exchange_bindings?user_id_type=open_id");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"admin_account\":\"email_admin_example@outlook.com\",\"exchange_account\":\"email_account_example@outlook.com\",\"user_id\":\"ou_xxxxxxxxxxxxxxxxxx\"}";
request.AddParameter("application/json", body,  ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
Console.WriteLine(response.Content);
```

