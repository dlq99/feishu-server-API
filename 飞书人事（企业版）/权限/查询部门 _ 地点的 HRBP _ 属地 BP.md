## 查询部门 / 地点的 HRBP / 属地 BP

通过部门或工作地点，查询对应的 HRBP / 属地 BP，返回的信息中包含BP的员工ID、部门ID、属地ID等信息。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/corehr/v1/security_groups/query` |
| HTTP Method | POST |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 查询部门/地点的HRBP/属地BP <br> 获取用户授权数据 <br> 获取核心人事信息 <br> 更新核心人事信息 |
| 权限要求 | corehr:authorization:read <br> corehr:corehr:readonly <br> corehr:corehr <br> corehr:authorization.bp:read |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| department_id_type | string | 否 | 此次调用中使用的部门 ID 类型 |
### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| item_list | bp_role_organization[] | 是 | 角色列表，一次最多支持查询 50 个 <br> **示例**:   |
| updated_at_gte | string | 否 | 授权时间大于 <br> **示例**: 1729773628  |
| updated_at_lte | string | 否 | 授权时间小于 <br> **示例**: 1729773628  |

**类型额外说明**:

- **bp_role_organization** 类型说明:

  基本属性:

   role_key: string <br> department_id: string <br> work_location_id: string <br>


**请求体示例**:

```json
{
    "item_list": [
        {
            "role_key": "location_bp",
            "department_id": "7063072995761456670",
            "work_location_id": "6892687221355185677"
        }
    ],
    "updated_at_gte": "1729773628",
    "updated_at_lte": "1729773628"
}
```

### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "hrbp_list": [
            {
                "employment_id_list": [
                    "['7063072995761456670']"
                ],
                "department_id": "7063072995761456670",
                "work_location_id": "6892687221355185677"
            }
        ]
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 400 | 1161403 | Incorrect parameter length | 请检查List，Map等容器类型参数 |
| 400 | 1161404 | Missing or invalid parameter | 请检查参数是否有效 |
| 400 | 1161406 | Parameter exceeds the optional range | 参数超过可选范围，请检查枚举类参数的可选范围 |
| 500 | 1161501 | System internal error | 请参考详细错误信息，如有问题请咨询[技术支持](https://applink.feishu.cn/TLJpeNdW) |

### 调用示例

#### Curl

```bash
curl -i -X POST 'https://open.feishu.cn/open-apis/corehr/v1/security_groups/query?department_id_type=people_corehr_department_id' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"item_list": [
		{
			"department_id": "7063072995761456670",
			"role_key": "location_bp",
			"work_location_id": "6892687221355185677"
		}
	],
	"updated_at_gte": "1729773628",
	"updated_at_lte": "1729773628"
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
	"github.com/larksuite/oapi-sdk-go/v3/service/corehr/v1"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkcorehr.NewQuerySecurityGroupReqBuilder().
		DepartmentIdType(`people_corehr_department_id`).
		Body(larkcorehr.NewQuerySecurityGroupReqBodyBuilder().
			ItemList([]*larkcorehr.BpRoleOrganization{
				larkcorehr.NewBpRoleOrganizationBuilder().
					RoleKey(`location_bp`).
					DepartmentId(`7063072995761456670`).
					WorkLocationId(`6892687221355185677`).
					Build(),
			}).
			UpdatedAtGte(`1729773628`).
			UpdatedAtLte(`1729773628`).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Corehr.V1.SecurityGroup.Query(context.Background(), req)

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
    request: QuerySecurityGroupRequest = QuerySecurityGroupRequest.builder() \
        .department_id_type("people_corehr_department_id") \
        .request_body(QuerySecurityGroupRequestBody.builder()
            .item_list([BpRoleOrganization.builder()
                .role_key("location_bp")
                .department_id("7063072995761456670")
                .work_location_id("6892687221355185677")
                .build()
                ])
            .updated_at_gte("1729773628")
            .updated_at_lte("1729773628")
            .build()) \
        .build()

    # 发起请求
    response: QuerySecurityGroupResponse = client.corehr.v1.security_group.query(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.corehr.v1.security_group.query failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
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
public class QuerySecurityGroupSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      QuerySecurityGroupReq req = QuerySecurityGroupReq.newBuilder()
             .departmentIdType("people_corehr_department_id")
             .querySecurityGroupReqBody(QuerySecurityGroupReqBody.newBuilder()
                 .itemList(new BpRoleOrganization[]{
                    BpRoleOrganization.newBuilder()
                      .roleKey("location_bp")
                      .departmentId("7063072995761456670")
                      .workLocationId("6892687221355185677")
                      .build()
                    })
                 .updatedAtGte("1729773628")
                 .updatedAtLte("1729773628")
                  .build())
             .build();

      // 发起请求
      QuerySecurityGroupResp resp = client.corehr().v1().securityGroup().query(req);

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

client.corehr.v1.securityGroup.query({
        params: {
                department_id_type:'people_corehr_department_id',
        },
        data: {
                item_list:[
                    {
                      role_key:'location_bp',
                      department_id:'7063072995761456670',
                      work_location_id:'6892687221355185677',
                      }
                    ],
                updated_at_gte:'1729773628',
                updated_at_lte:'1729773628',
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
var client = new RestClient("https://open.feishu.cn/open-apis/corehr/v1/security_groups/query?department_id_type=people_corehr_department_id");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"item_list\":[{\"department_id\":\"7063072995761456670\",\"role_key\":\"location_bp\",\"work_location_id\":\"6892687221355185677\"}],\"updated_at_gte\":\"1729773628\",\"updated_at_lte\":\"1729773628\"}";
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
    "item_list": [
        {
            "role_key": "location_bp",
            "department_id": "7063072995761456670",
            "work_location_id": "6892687221355185677"
        }
    ],
    "updated_at_gte": "1729773628",
    "updated_at_lte": "1729773628"
}';
$request = new Request('POST', 'https://open.feishu.cn/open-apis/corehr/v1/security_groups/query?department_id_type=people_corehr_department_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

