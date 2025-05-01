## 更新部门ID

调用该接口可以更新部门的自定义 ID，即 department_id。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/contact/v3/departments/:department_id/update_department_id` |
| HTTP Method | PATCH |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom |
| 权限要求 | 更新部门 ID |
| 权限要求 | contact:contact:update_department_id |

### 路径参数

| 参数名 | 类型 |  描述 |
| ------ | ---- | ---- |
| department_id | string | 需要更新自定义 ID 的部门 ID，该 ID 类型需要与查询参数 department_id_type 的取值一致。ID 获取方式说明：

- 调用[创建部门](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/create)接口后，可从返回结果中获取到部门 ID 信息。
- 部门 API 提供了多种获取其他部门 ID 的方式，如[获取子部门列表](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/children)、[获取父部门信息](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/parent)、[搜索部门](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/search)，你可以选择合适的 API 进行查询。 |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| department_id_type | string | 否 | 此次调用中的部门 ID 类型。关于部门 ID 的详细介绍，可参见[部门 ID 说明](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview#23857fe0)。

**默认值**：open_department_id |
### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| new_department_id | string | 是 | 新的自定义部门 ID，即部门的 department_id。<br><br>**注意**：<br><br>- 不能以 `od-` 开头。<br>- 不能设置为 `0`。<br>- 不能与其他未删除部门的 department_id 重复。 <br> **示例**: NewDevDepartID <br> **数据校验规则**:<br>最大长度: 128 |

**请求体示例**:

```json
{
    "new_department_id": "NewDevDepartID"
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
| 400 | 40001 | invalid params | 参数错误，请对照接口文档修改输入参数后重试。 |
| 400 | 43009 | exceed update custom dept limit error | 超过最大更新限制。 |
| 403 | 40007 | can not update dept custom id error | 无法更新部门自定义 ID。你需要在应用的通讯录权限范围内添加当前操作的部门。了解应用的通讯录权限范围，可参见[权限范围资源介绍](/ssl:ttdoc/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority)。 |
| 401 | 42008 | tenant id is invalid error | 租户身份无效。请求时，请确保设置的请求头 Authorization 与待操作资源同属一个租户下。 |

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
    request: UpdateDepartmentIdDepartmentRequest = UpdateDepartmentIdDepartmentRequest.builder() \
        .department_id("od-d6b83d25c129775723a36f52495c4f81") \
        .department_id_type("open_department_id") \
        .request_body(UpdateDepartmentIdDepartmentRequestBody.builder()
            .new_department_id("NewDevDepartID")
            .build()) \
        .build()

    # 发起请求
    response: UpdateDepartmentIdDepartmentResponse = client.contact.v3.department.update_department_id(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.contact.v3.department.update_department_id failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
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
public class UpdateDepartmentIdDepartmentSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      UpdateDepartmentIdDepartmentReq req = UpdateDepartmentIdDepartmentReq.newBuilder()
             .departmentId("od-d6b83d25c129775723a36f52495c4f81")
             .departmentIdType("open_department_id")
             .updateDepartmentIdDepartmentReqBody(UpdateDepartmentIdDepartmentReqBody.newBuilder()
                 .newDepartmentId("NewDevDepartID")
                  .build())
             .build();

      // 发起请求
      UpdateDepartmentIdDepartmentResp resp = client.contact().v3().department().updateDepartmentId(req);

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

client.contact.v3.department.updateDepartmentId({
        path: {
                department_id:'od-d6b83d25c129775723a36f52495c4f81',
        },
        params: {
                department_id_type:'open_department_id',
        },
        data: {
                new_department_id:'NewDevDepartID',
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
var client = new RestClient("https://open.feishu.cn/open-apis/contact/v3/departments/od-d6b83d25c129775723a36f52495c4f81/update_department_id?department_id_type=open_department_id");
client.Timeout = -1;
var request = new RestRequest(Method.PATCH);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"new_department_id\":\"NewDevDepartID\"}";
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
    "new_department_id": "NewDevDepartID"
}';
$request = new Request('PATCH', 'https://open.feishu.cn/open-apis/contact/v3/departments/od-d6b83d25c129775723a36f52495c4f81/update_department_id?department_id_type=open_department_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X PATCH 'https://open.feishu.cn/open-apis/contact/v3/departments/od-d6b83d25c129775723a36f52495c4f81/update_department_id?department_id_type=open_department_id' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"new_department_id": "NewDevDepartID"
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
	req := larkcontact.NewUpdateDepartmentIdDepartmentReqBuilder().
		DepartmentId(`od-d6b83d25c129775723a36f52495c4f81`).
		DepartmentIdType(`open_department_id`).
		Body(larkcontact.NewUpdateDepartmentIdDepartmentReqBodyBuilder().
			NewDepartmentId(`NewDevDepartID`).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Contact.V3.Department.UpdateDepartmentId(context.Background(), req)

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

