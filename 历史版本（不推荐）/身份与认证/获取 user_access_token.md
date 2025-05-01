## 获取 user_access_token

:::html
<md-alert type="error">
本接口已成为历史版本，不再维护更新，不推荐使用。请使用最新版本：[获取 user_access_token ](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/authentication-management/access-token/get-user-access-token)
</md-alert>。
:::

根据[登录预授权码](/ssl:ttdoc/common-capabilities/sso/api/obtain-oauth-code) 返回 code 获取 `user_access_token`。



💡 
 - 为了让流程更加规范，本接口不再返回用户信息，只返回token相关的字段。如需用户信息，请通过 [获取用户信息](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/authen-v1/user_info/get)接口获取数据。
- user_access_token 有效期为 2 小时左右，具体剩余有效期可通过当前接口返回的 expires_in 参数获取。如果 user_access_token 过期可以[刷新 user_access_token](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/authen-v1/oidc-refresh_access_token/create)。当前接口返回结果中包含用于刷新 user_access_token 的 refresh_token 参数，注意该参数也存在有效期（30 天左右），具体剩余有效期可通过返回的 refresh_expires_in 参数获取。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/authen/v1/oidc/access_token` |
| HTTP Method | POST |
| 支持的访问令牌 | app_access_token |
| 支持的应用类型 | custom  isv |

### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| grant_type | string | 是 | 授权类型，**固定值** <br> **示例**: authorization_code  |
| code | string | 是 | 登录预授权码，调用[登录预授权码](/ssl:ttdoc/common-capabilities/sso/api/obtain-oauth-code) 获取code <br> **示例**: xMSldislSkdK  |

**请求体示例**:

```json
{
    "grant_type": "authorization_code",
    "code": "xMSldislSkdK"
}
```

### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "access_token": "u-5Dak9ZAxJ9tFUn8MaTD_BFM51FNdg5xzO0y010000HWb",
        "refresh_token": "ur-6EyFQZyplb9URrOx5NtT_HM53zrJg59HXwy040400G.e",
        "token_type": "Bearer",
        "expires_in": 7199,
        "refresh_expires_in": 2591999,
        "scope": "auth:user.id:read bitable:app"
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 200 | 20001 | Invalid request. Please check request param | 请检查请求参数 |
| 200 | 20002 | The app_id or app_secret passed is incorrect. Please check the value | 检查app_id和密钥是否正确 |
| 200 | 20003 | The code passed is invalid. Please note that the code could only be used once | 登录预授权码的有效期是 5 分钟，且只能被使用一次。请检查登录预授权码是否被重复使用或过期 |
| 200 | 20004 | The code passed has expired. Please generate a new one | 过期code，请重新生成 |
| 200 | 20007 | Failed to generate a user access token. Please try again | 请检查参数是否有效，重试 |
| 200 | 20008 | User not exist | 用户不存在，换有效帐号 |
| 200 | 20013 | The tenant access token passed is invalid. Please check the value | 检查tenant_access_token是否有效 |
| 200 | 20014 | The app access token passed is invalid. Please check the value | 检查app_access_token是否有效 |
| 200 | 20021 | User resigned | 用户离职，请使用有效帐号 |
| 200 | 20022 | User frozen | 用户冻结，请使用有效帐号 |
| 200 | 20023 | User not registered | 用户未注册，请使用有效帐号 |
| 200 | 20024 | App id in user_access_token or refresh_token diff with app id in app_access_token or tenant_access_token. Please keep the app id consistent | 请检查生成两个token的app是否为同一个 |
| 200 | 20025 | Lack of app_id or app_secret in request | 缺失app_id或app_secret，请检查参数 |
| 200 | 20028 | Invalid app id | 无效app_id，请检查参数 |
| 200 | 20029 | Invalid redirect uri | redirect_uri 无效。排查方案：<br><br>1. 确保 Authorization 取值正确。例如，实际开发的应用 A，但调用 API 时却使用了应用 B 的 app_access_token。<br>2. 确保[获取登录授权码 code](/ssl:ttdoc/common-capabilities/sso/api/obtain-oauth-code) 时，设置的回调地址 redirect_uri 参数，已配置到开发者后台 > 应用详情页 > 安全设置 > 重定向 URL。<br><br>关于该报错的详细解决方案，参见[如何解决授权免登页面 20029 错误](/ssl:ttdoc/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-resolve-the-authorization-page-20029-error)。 |
| 200 | 20035 | The app_id or app_secret passed is incorrect. Please check the value | 无效app_id 或 app_secret，请检查参数 |
| 200 | 20036 | The grant_type passed is not supported | 无效grant_type，请与接口要求保持一致 |
| 200 | 20039 | The user access token is not found. Please check the value | 查询不到user_access_token，请传有效参数 |
| 200 | 20042 | App disabled | app不可用，请检查app状态 |
| 200 | 20046 | Brand inconsistency | 应用品牌和域名品牌不一致，请保证feishu应用在feishu域名下使用，lark类似 |

### 调用示例

#### Java SDK

```java
package com.lark.oapi.sample.apiall.authenv1;
import com.google.gson.JsonParser;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.authen.v1.model.*;
import java.util.HashMap;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class CreateOidcAccessTokenSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      CreateOidcAccessTokenReq req = CreateOidcAccessTokenReq.newBuilder()
             .createOidcAccessTokenReqBody(CreateOidcAccessTokenReqBody.newBuilder()
                 .grantType("authorization_code")
                 .code("xMSldislSkdK")
                  .build())
             .build();

      // 发起请求
      CreateOidcAccessTokenResp resp = client.authen().v1().oidcAccessToken().create(req);

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

client.authen.v1.oidcAccessToken.create({
        data: {
                grant_type:'authorization_code',
                code:'xMSldislSkdK',
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
var client = new RestClient("https://open.feishu.cn/open-apis/authen/v1/oidc/access_token");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"code\":\"xMSldislSkdK\",\"grant_type\":\"authorization_code\"}";
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
    "grant_type": "authorization_code",
    "code": "xMSldislSkdK"
}';
$request = new Request('POST', 'https://open.feishu.cn/open-apis/authen/v1/oidc/access_token', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X POST 'https://open.feishu.cn/open-apis/authen/v1/oidc/access_token' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"code": "xMSldislSkdK",
	"grant_type": "authorization_code"
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
	"github.com/larksuite/oapi-sdk-go/v3/service/authen/v1"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkauthen.NewCreateOidcAccessTokenReqBuilder().
		Body(larkauthen.NewCreateOidcAccessTokenReqBodyBuilder().
			GrantType(`authorization_code`).
			Code(`xMSldislSkdK`).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Authen.V1.OidcAccessToken.Create(context.Background(), req)

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
from lark_oapi.api.authen.v1 import *


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
    request: CreateOidcAccessTokenRequest = CreateOidcAccessTokenRequest.builder() \
        .request_body(CreateOidcAccessTokenRequestBody.builder()
            .grant_type("authorization_code")
            .code("xMSldislSkdK")
            .build()) \
        .build()

    # 发起请求
    response: CreateOidcAccessTokenResponse = client.authen.v1.oidc_access_token.create(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.authen.v1.oidc_access_token.create failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

