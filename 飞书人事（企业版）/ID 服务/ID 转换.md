## ID 转换

该接口用来进行飞书人事和飞书通讯录、people admin 的各种 ID 转换（仅适用于飞书人事新链路租户）

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/corehr/v1/common_data/id/convert` |
| HTTP Method | POST |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom |
| 权限要求 | 获取 ID 转换信息 <br> 获取用户 user ID |
| 权限要求 | corehr:common_data.id.convert:read |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| id_transform_type | integer | 是 | ID 转换类型 |
| id_type | string | 是 | 要转换的ID类型 |
| feishu_user_id_type | string | 否 | 用户 ID 类型 |
| feishu_department_id_type | string | 否 | 此次调用中使用的部门 ID 类型 |
### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| ids | undefined[] | 是 | ID 列表（最多传入 100 个 ID，ID 长度限制 50 个字符） <br> **示例**:  <br> **数据校验规则**:<br>最大长度: 100最小长度: 1 |

**请求体示例**:

```json
{
    "ids": [
        "6891251722631891445"
    ]
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
                "id": "7224321696097404460",
                "target_id": "7224321696097404461"
            }
        ]
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 400 | 1160001 | Param Invalid | 请检查参数是否符合 |

### 调用示例

#### Golang SDK

```go
package main

import (
	"context"
	"fmt"
	"github.com/larksuite/oapi-sdk-go/v3"
	"github.com/larksuite/oapi-sdk-go/v3/core"
	"github.com/larksuite/oapi-sdk-go/v3/service/corehr/v1"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkcorehr.NewConvertCommonDataIdReqBuilder().
		IdTransformType(1).
		IdType(`user_id`).
		FeishuUserIdType(`open_id`).
		FeishuDepartmentIdType(`open_department_id`).
		Body(larkcorehr.NewConvertCommonDataIdReqBodyBuilder().
			Ids([]string{`6891251722631891445`}).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Corehr.V1.CommonDataId.Convert(context.Background(), req)

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
from lark_oapi.api.corehr.v1 import *


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
    request: ConvertCommonDataIdRequest = ConvertCommonDataIdRequest.builder() \
        .id_transform_type(1) \
        .id_type("user_id") \
        .feishu_user_id_type("open_id") \
        .feishu_department_id_type("open_department_id") \
        .request_body(ConvertCommonDataIdRequestBody.builder()
            .ids(["6891251722631891445"])
            .build()) \
        .build()

    # 发起请求
    response: ConvertCommonDataIdResponse = client.corehr.v1.common_data_id.convert(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.corehr.v1.common_data_id.convert failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

#### Java SDK

```java
package com.lark.oapi.sample.apiall.corehrv1;
import com.google.gson.JsonParser;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.corehr.v1.model.*;
import java.util.HashMap;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class ConvertCommonDataIdSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      ConvertCommonDataIdReq req = ConvertCommonDataIdReq.newBuilder()
             .idTransformType(1)
             .idType("user_id")
             .feishuUserIdType("open_id")
             .feishuDepartmentIdType("open_department_id")
             .convertCommonDataIdReqBody(ConvertCommonDataIdReqBody.newBuilder()
                 .ids(new String[]{"6891251722631891445"})
                  .build())
             .build();

      // 发起请求
      ConvertCommonDataIdResp resp = client.corehr().v1().commonDataId().convert(req);

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

client.corehr.v1.commonDataId.convert({
        params: {
                id_transform_type:1,
                id_type:'user_id',
                feishu_user_id_type:'open_id',
                feishu_department_id_type:'open_department_id',
        },
        data: {
                ids:['6891251722631891445'],
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
var client = new RestClient("https://open.feishu.cn/open-apis/corehr/v1/common_data/id/convert?feishu_department_id_type=open_department_id&feishu_user_id_type=open_id&id_transform_type=1&id_type=user_id");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"ids\":[\"6891251722631891445\"]}";
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
    "ids": [
        "6891251722631891445"
    ]
}';
$request = new Request('POST', 'https://open.feishu.cn/open-apis/corehr/v1/common_data/id/convert?feishu_department_id_type=open_department_id&feishu_user_id_type=open_id&id_transform_type=1&id_type=user_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X POST 'https://open.feishu.cn/open-apis/corehr/v1/common_data/id/convert?feishu_department_id_type=open_department_id&feishu_user_id_type=open_id&id_transform_type=1&id_type=user_id' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"ids": [
		"6891251722631891445"
	]
}'
```

