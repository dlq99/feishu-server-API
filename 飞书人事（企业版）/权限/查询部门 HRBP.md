## 查询部门 HRBP

查询部门的 HRBP 信息，包括来自上级部门的 HRBP。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/corehr/v2/bps/get_by_department` |
| HTTP Method | POST |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 查看部门 BP 信息 <br> 获取用户 user ID |
| 权限要求 | corehr:bp.get_by_department:read |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| user_id_type | string | 否 | 用户 ID 类型 |
| department_id_type | string | 否 | 此次调用中使用的部门 ID 类型 |
### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| department_id | string | 是 | 部门 ID，ID类型与department_id_type的取值意义一致。<br>  > <br>可以使用 [ID转换服务](https://open.larkoffice.com/document/uAjLw4CM/ukTMukTMukTM/reference/corehr-v1/common_data-id/convert)换取 ==department_id==<br>  > <br>部门id也可通过[搜索部门信息](https://open.larkoffice.com/document/server-docs/corehr-v1/organization-management/department/search)接口获取。 <br> **示例**: 6893014062142064111  |

**请求体示例**:

```json
{
    "department_id": "6893014062142064111"
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
                "department_id": "4719456877659520852",
                "hrbp_ids": [
                    "4719456877659520852"
                ]
            }
        ]
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 400 | 1161401 | Incorrect parameter type | 请检查字符串、数字等的参数类型 |
| 400 | 1161402 | Incorrect parameter range | 请检查数字类型参数是否超出约定范围 |
| 400 | 1161403 | Incorrect parameter length | 请检查List，Map等容器类型参数 |
| 400 | 1161404 | Missing or invalid parameter | 请检查参数是否有效 |
| 400 | 1161405 | Parameter parsing error | 请检查请求体json格式是否正确 |
| 400 | 1161406 | Parameter exceeds the optional range | 请检查枚举类参数的可选范围 |
| 500 | 1161501 | System internal error | 请参考详细错误信息，如有问题请咨询[技术支持](https://applink.feishu.cn/TLJpeNdW) |

### 调用示例

#### Python SDK

```python
import json

import lark_oapi as lark
from lark_oapi.api.corehr.v2 import *


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
    request: GetByDepartmentBpRequest = GetByDepartmentBpRequest.builder() \
        .user_id_type("open_id") \
        .department_id_type("open_department_id") \
        .request_body(GetByDepartmentBpRequestBody.builder()
            .department_id("6893014062142064111")
            .build()) \
        .build()

    # 发起请求
    response: GetByDepartmentBpResponse = client.corehr.v2.bp.get_by_department(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.corehr.v2.bp.get_by_department failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

#### Java SDK

```java
package com.lark.oapi.sample.apiall.corehrv2;
import com.google.gson.JsonParser;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.corehr.v2.model.*;
import java.util.HashMap;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class GetByDepartmentBpSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      GetByDepartmentBpReq req = GetByDepartmentBpReq.newBuilder()
             .userIdType("open_id")
             .departmentIdType("open_department_id")
             .getByDepartmentBpReqBody(GetByDepartmentBpReqBody.newBuilder()
                 .departmentId("6893014062142064111")
                  .build())
             .build();

      // 发起请求
      GetByDepartmentBpResp resp = client.corehr().v2().bp().getByDepartment(req);

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

client.corehr.v2.bp.getByDepartment({
        params: {
                user_id_type:'open_id',
                department_id_type:'open_department_id',
        },
        data: {
                department_id:'6893014062142064111',
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
var client = new RestClient("https://open.feishu.cn/open-apis/corehr/v2/bps/get_by_department?department_id_type=open_department_id&user_id_type=open_id");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"department_id\":\"6893014062142064111\"}";
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
    "department_id": "6893014062142064111"
}';
$request = new Request('POST', 'https://open.feishu.cn/open-apis/corehr/v2/bps/get_by_department?department_id_type=open_department_id&user_id_type=open_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X POST 'https://open.feishu.cn/open-apis/corehr/v2/bps/get_by_department?department_id_type=open_department_id&user_id_type=open_id' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"department_id": "6893014062142064111"
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
	"github.com/larksuite/oapi-sdk-go/v3/service/corehr/v2"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkcorehr.NewGetByDepartmentBpReqBuilder().
		UserIdType(`open_id`).
		DepartmentIdType(`open_department_id`).
		Body(larkcorehr.NewGetByDepartmentBpReqBodyBuilder().
			DepartmentId(`6893014062142064111`).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Corehr.V2.Bp.GetByDepartment(context.Background(), req)

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

