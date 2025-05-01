## 更新用户ID

调用该接口更新用户的 user_id。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/contact/v3/users/:user_id/update_user_id` |
| HTTP Method | PATCH |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom |
| 权限要求 | 获取用户 user ID <br> 更新用户 ID |
| 权限要求 | contact:contact:update_user_id |

### 路径参数

| 参数名 | 类型 |  描述 |
| ------ | ---- | ---- |
| user_id | string | 用户 ID，ID 类型与查询参数 user_id_type 的取值保持一致。 |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| user_id_type | string | 否 | 用户 ID 类型 |
### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| new_user_id | string | 是 | 自定义新的用户 user_id。长度不能超过 64 字符。 <br> **示例**: 3e3cf96b  |

**请求体示例**:

```json
{
    "new_user_id": "3e3cf96b"
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
| 400 | 40001 | Invalid params | 参数错误。请参考接口文档的参数描述，检查输入参数是否填写有误。 |
| 400 | 41009 | no email or mobile error | 无邮箱或者手机号，请添加后重试。 |
| 400 | 41011 | userID already exist error | 用户的 user_id 已存在，你需要更换 ID 并重试。 |
| 400 | 41013 | exceed userID update limit error | 超过用户 ID 更新次数限制。 |
| 400 | 41050 | no user authority error | 无用户权限。当前操作的用户需在应用的通讯录权限范围内。通讯录权限范围的介绍与设置方式，参见[权限范围资源介绍](/ssl:ttdoc/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority)。 |
| 400 | 41054 | new user id is required  error | 更新后的 user_id 错误。请更换 user_id 值后重试。 |

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
    request: UpdateUserIdUserRequest = UpdateUserIdUserRequest.builder() \
        .user_id("ou-938e3e4fdc5e1993bee01250076f0cc2") \
        .user_id_type("open_id") \
        .request_body(UpdateUserIdUserRequestBody.builder()
            .new_user_id("3e3cf96b")
            .build()) \
        .build()

    # 发起请求
    response: UpdateUserIdUserResponse = client.contact.v3.user.update_user_id(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.contact.v3.user.update_user_id failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
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
public class UpdateUserIdUserSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      UpdateUserIdUserReq req = UpdateUserIdUserReq.newBuilder()
             .userId("ou-938e3e4fdc5e1993bee01250076f0cc2")
             .userIdType("open_id")
             .updateUserIdUserReqBody(UpdateUserIdUserReqBody.newBuilder()
                 .newUserId("3e3cf96b")
                  .build())
             .build();

      // 发起请求
      UpdateUserIdUserResp resp = client.contact().v3().user().updateUserId(req);

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

client.contact.v3.user.updateUserId({
        path: {
                user_id:'ou-938e3e4fdc5e1993bee01250076f0cc2',
        },
        params: {
                user_id_type:'open_id',
        },
        data: {
                new_user_id:'3e3cf96b',
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
var client = new RestClient("https://open.feishu.cn/open-apis/contact/v3/users/ou-938e3e4fdc5e1993bee01250076f0cc2/update_user_id?user_id_type=open_id");
client.Timeout = -1;
var request = new RestRequest(Method.PATCH);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"new_user_id\":\"3e3cf96b\"}";
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
    "new_user_id": "3e3cf96b"
}';
$request = new Request('PATCH', 'https://open.feishu.cn/open-apis/contact/v3/users/ou-938e3e4fdc5e1993bee01250076f0cc2/update_user_id?user_id_type=open_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X PATCH 'https://open.feishu.cn/open-apis/contact/v3/users/ou-938e3e4fdc5e1993bee01250076f0cc2/update_user_id?user_id_type=open_id' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"new_user_id": "3e3cf96b"
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
	req := larkcontact.NewUpdateUserIdUserReqBuilder().
		UserId(`ou-938e3e4fdc5e1993bee01250076f0cc2`).
		UserIdType(`open_id`).
		Body(larkcontact.NewUpdateUserIdUserReqBodyBuilder().
			NewUserId(`3e3cf96b`).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Contact.V3.User.UpdateUserId(context.Background(), req)

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

