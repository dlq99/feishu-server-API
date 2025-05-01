## 获取 user_access_token（v1 版本）

:::html
<md-alert type="error">
本接口已成为历史版本，不再维护更新，不推荐使用。请使用最新版本：[获取 user_access_token ](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/authentication-management/access-token/get-user-access-token)
</md-alert>。
:::

根据[登录预授权码](/ssl:ttdoc/ukTMukTMukTM/ukzN4UjL5cDO14SO3gTN) code 获取 `user_access_token`。

💡 
 本接口用于网页应用免登录应用场景，小程序应用获取 user_access_token 的方法，请参考小程序应用提供的 [code2session](/ssl:ttdoc/uYjL24iN/ukjM04SOyQjL5IDN) 接口。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/authen/v1/access_token` |
| HTTP Method | POST |
| 支持的访问令牌 | app_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 获取用户邮箱信息 <br> 获取用户 user ID <br> 获取用户手机号 <br> 获取用户受雇信息 |

### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| grant_type | string | 是 | 授权类型，**固定值**： <br> **示例**: authorization_code  |
| code | string | 是 | 登录预授权码，调用[获取登录预授权码](/ssl:ttdoc/ukTMukTMukTM/ukzN4UjL5cDO14SO3gTN)接口获取 <br> **示例**: xMSldislSkdK  |

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
        "access_token": "u-Q7JWnaIM_kRChuLfreHmpArjOEayt.5XUBJcZr.V0Gst4FdQCtvrd9sAViLXQnQgkpL19brGOjKZQTxb",
        "token_type": "Bearer",
        "expires_in": 7140,
        "name": "zhangsan",
        "en_name": "Three Zhang",
        "avatar_url": "www.feishu.cn/avatar/icon",
        "avatar_thumb": "www.feishu.cn/avatar/icon_thumb",
        "avatar_middle": "www.feishu.cn/avatar/icon_middle",
        "avatar_big": "www.feishu.cn/avatar/icon_big",
        "open_id": "ou_caecc734c2e3328a62489fe0648c4b98779515d3",
        "union_id": "on_d89jhsdhjsajkda7828enjdj328ydhhw3u43yjhdj",
        "email": "zhangsan@feishu.cn",
        "enterprise_email": "demo@mail.com",
        "user_id": "5d9bdxxx",
        "mobile": "+86130002883xx",
        "tenant_key": "736588c92lxf175d",
        "refresh_expires_in": 2591940,
        "refresh_token": "ur-oQ0mMq6MCcueAv0pwx2fQQhxqv__CbLu6G8ySFwafeKww2Def2BJdOkW3.9gCFM.LBQgFri901QaqeuL",
        "sid": "AAAAAAAAAANjgHsqKEAAEw=="
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 200 | 20001 | Invalid request. Please check request param | 请检查请求参数 |
| 200 | 20007 | Failed to generate a user access token. Please try again | 生成失败，请检查参数是否有效，重试 |
| 200 | 20008 | User not exist | 用户不存在，换有效帐号 |
| 200 | 20009 | Tenant does not install app | 租户没有安装app，请联系租户管理员安装 |
| 200 | 20021 | User resigned | 用户离职，请使用有效帐号 |
| 200 | 20022 | User frozen | 用户冻结，请使用有效帐号 |
| 200 | 20023 | User not registered | 用户未注册，请使用有效帐号 |
| 200 | 20024 | App id in user_access_token or refresh_token diff with app id in app_access_token or tenant_access_token. Please keep the app id consistent | 请检查生成两个token的app是否为同一个 |
| 200 | 20025 | Lack of app_id or app_secret in request | 缺失app_id或app_secret，请检查参数 |
| 200 | 20028 | Invalid app id | 无效app_id，请检查参数 |
| 500 | 20050 | System error | 系统错误，请重试 |

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

client.authen.v1.accessToken.create({
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
var client = new RestClient("https://open.feishu.cn/open-apis/authen/v1/access_token");
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
$request = new Request('POST', 'https://open.feishu.cn/open-apis/authen/v1/access_token', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X POST 'https://open.feishu.cn/open-apis/authen/v1/access_token' \
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
	req := larkauthen.NewCreateAccessTokenReqBuilder().
		Body(larkauthen.NewCreateAccessTokenReqBodyBuilder().
			GrantType(`authorization_code`).
			Code(`xMSldislSkdK`).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Authen.V1.AccessToken.Create(context.Background(), req)

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
    request: CreateAccessTokenRequest = CreateAccessTokenRequest.builder() \
        .request_body(CreateAccessTokenRequestBody.builder()
            .grant_type("authorization_code")
            .code("xMSldislSkdK")
            .build()) \
        .build()

    # 发起请求
    response: CreateAccessTokenResponse = client.authen.v1.access_token.create(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.authen.v1.access_token.create failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
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
public class CreateAccessTokenSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      CreateAccessTokenReq req = CreateAccessTokenReq.newBuilder()
             .createAccessTokenReqBody(CreateAccessTokenReqBody.newBuilder()
                 .grantType("authorization_code")
                 .code("xMSldislSkdK")
                  .build())
             .build();

      // 发起请求
      CreateAccessTokenResp resp = client.authen().v1().accessToken().create(req);

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

