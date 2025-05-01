## 刷新 user_access_token

:::html
<md-alert type="error">
本接口已成为历史版本，不再维护更新，不推荐使用。请使用最新版本：[刷新 user_access_token ](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/authentication-management/access-token/refresh-user-access-token)
</md-alert>。
:::

user_access_token 的最大有效期是 2小时左右。当 user_access_token 过期时，可以调用本接口获取新的 user_access_token。

💡 
 调用本接口刷新 user_access_token 后，请更新你本地保存的 user_access_token 以及用于刷新 token 的 refresh_token 参数值，不要继续使用旧值重复刷新，否则可能会因为 token 失效导致接口调用失败。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/authen/v1/oidc/refresh_access_token` |
| HTTP Method | POST |
| 支持的访问令牌 | app_access_token |
| 支持的应用类型 | custom  isv |

### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| grant_type | string | 是 | 授权类型，**固定值**： <br> **示例**: refresh_token  |
| refresh_token | string | 是 | 刷新和获取user_access_token接口均返回 `refresh_token`，**每次请求，请注意使用最新获取到的`refresh_token`** <br> **示例**: ur-h4_5nUXdJ4O8rqfGe.YJCwM13Gjc557xUG20hkk00f7K  |

**请求体示例**:

```json
{
    "grant_type": "refresh_token",
    "refresh_token": "ur-h4_5nUXdJ4O8rqfGe.YJCwM13Gjc557xUG20hkk00f7K"
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
| 200 | 20007 | Failed to generate a user access token. Please try again | 请检查参数是否有效，重试 |
| 200 | 20008 | User not exist | 用户不存在，换有效帐号 |
| 200 | 20013 | The tenant access token passed is invalid. Please check the value | 检查tenant_access_token是否有效 |
| 200 | 20014 | The app access token passed is invalid. Please check the value | 检查app_access_token是否有效 |
| 200 | 20021 | User resigned | 用户离职，请使用有效帐号 |
| 200 | 20022 | User frozen | 用户冻结，请使用有效帐号 |
| 200 | 20023 | User not registered | 用户未注册，请使用有效帐号 |
| 200 | 20024 | App id in user_access_token or refresh_token diff with app id in app_access_token or tenant_access_token. Please keep the app id consistent | 请检查生成两个token的app是否为同一个 |
| 200 | 20026 | The refresh token passed is invalid. Please check the value | 无效refresh_token，请检查是否过期或已经消费 |
| 200 | 20028 | Invalid app id | 无效app_id，请检查参数 |
| 200 | 20029 | Invalid redirect uri | redirect_uri 无效。排查方案：<br><br>1. 确保 Authorization 取值正确。例如，实际开发的应用 A，但调用 API 时却使用了应用 B 的 app_access_token。<br>2. 确保[获取登录授权码 code](/ssl:ttdoc/common-capabilities/sso/api/obtain-oauth-code) 时，设置的回调地址 redirect_uri 参数，已配置到开发者后台 > 应用详情页 > 安全设置 > 重定向 URL。<br><br>关于该报错的详细解决方案，参见[如何解决授权免登页面 20029 错误](/ssl:ttdoc/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-resolve-the-authorization-page-20029-error)。 |
| 200 | 20036 | The grant_type passed is not supported | 无效grant_type，请与接口要求保持一致 |
| 200 | 20037 | The refresh token passed has expired. Please generate a new one | 过期refresh_token，请传有效参数 |
| 200 | 20038 | The refresh token passed is not found. Please check the value | 查询不到 refresh_token。<br><br>当你使用 refresh_token 刷新 user_access_token 后，需要保存返回结果中新的 refresh_token 供下次刷新使用。<br><br>如果下次刷新时重复使用旧的 refresh_token 或者 refresh_token 已过期，则会报该错误。refresh_token 有效期为 30 天左右，具体时间可通过接口返回的 refresh_expires_in 参数获取。<br><br>你可以调用[获取 user_access_token](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/authen-v1/oidc-access_token/create)重新获取 user_access_token 和 refresh_token。 |
| 200 | 20042 | App disabled | app不可用，请检查app状态 |
| 200 | 20046 | Brand inconsistency | 应用品牌和域名品牌不一致，请保证feishu应用在feishu域名下使用，lark类似 |

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

client.authen.v1.oidcRefreshAccessToken.create({
        data: {
                grant_type:'refresh_token',
                refresh_token:'ur-h4_5nUXdJ4O8rqfGe.YJCwM13Gjc557xUG20hkk00f7K',
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
var client = new RestClient("https://open.feishu.cn/open-apis/authen/v1/oidc/refresh_access_token");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"grant_type\":\"refresh_token\",\"refresh_token\":\"ur-h4_5nUXdJ4O8rqfGe.YJCwM13Gjc557xUG20hkk00f7K\"}";
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
    "grant_type": "refresh_token",
    "refresh_token": "ur-h4_5nUXdJ4O8rqfGe.YJCwM13Gjc557xUG20hkk00f7K"
}';
$request = new Request('POST', 'https://open.feishu.cn/open-apis/authen/v1/oidc/refresh_access_token', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X POST 'https://open.feishu.cn/open-apis/authen/v1/oidc/refresh_access_token' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"grant_type": "refresh_token",
	"refresh_token": "ur-h4_5nUXdJ4O8rqfGe.YJCwM13Gjc557xUG20hkk00f7K"
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
	req := larkauthen.NewCreateOidcRefreshAccessTokenReqBuilder().
		Body(larkauthen.NewCreateOidcRefreshAccessTokenReqBodyBuilder().
			GrantType(`refresh_token`).
			RefreshToken(`ur-h4_5nUXdJ4O8rqfGe.YJCwM13Gjc557xUG20hkk00f7K`).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Authen.V1.OidcRefreshAccessToken.Create(context.Background(), req)

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
    request: CreateOidcRefreshAccessTokenRequest = CreateOidcRefreshAccessTokenRequest.builder() \
        .request_body(CreateOidcRefreshAccessTokenRequestBody.builder()
            .grant_type("refresh_token")
            .refresh_token("ur-h4_5nUXdJ4O8rqfGe.YJCwM13Gjc557xUG20hkk00f7K")
            .build()) \
        .build()

    # 发起请求
    response: CreateOidcRefreshAccessTokenResponse = client.authen.v1.oidc_refresh_access_token.create(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.authen.v1.oidc_refresh_access_token.create failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

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
public class CreateOidcRefreshAccessTokenSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      CreateOidcRefreshAccessTokenReq req = CreateOidcRefreshAccessTokenReq.newBuilder()
             .createOidcRefreshAccessTokenReqBody(CreateOidcRefreshAccessTokenReqBody.newBuilder()
                 .grantType("refresh_token")
                 .refreshToken("ur-h4_5nUXdJ4O8rqfGe.YJCwM13Gjc557xUG20hkk00f7K")
                  .build())
             .build();

      // 发起请求
      CreateOidcRefreshAccessTokenResp resp = client.authen().v1().oidcRefreshAccessToken().create(req);

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

