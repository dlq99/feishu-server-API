## 根据流程 ID 查询组织架构调整记录

用户通过『飞书人事-我的团队-组织架构』 发起一个组织架构调整会根据 审批流配置发起 一个或多个审批。  之后用户可通过流程 process 的单据 ID， 查询到该审批进行的状态， 以及该流程中涉及到的 组织架构信息（包括部门变更、人员变更记录 ID、岗位变更记录 ID）。
如需查询具体变更详情：

- 部门变更：[批量查询部门变更接口](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/corehr-v2/approval_groups/open_query_department_change_list_by_ids)

- 员工变更：[批量查询员工变更接口](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/corehr-v2/approval_groups/open_query_job_change_list_by_ids)

⚠️ 
 - 用户使用该接口前需提前获取 组织架构调整流程信息 权限
- 延迟说明：数据库主从延迟2s以内，即：用户接收到流程状态变更消息后2s内调用此接口可能查询不到数据。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/corehr/v2/approval_groups/:process_id` |
| HTTP Method | GET |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 获取用户 user ID <br> 获取组织架构调整流程信息 |
| 权限要求 | corehr:approval_groups:read |

### 路径参数

| 参数名 | 类型 |  描述 |
| ------ | ---- | ---- |
| process_id | string | 组织架构调整流程 ID， 用户通过『飞书人事-我的团队-组织架构』或『飞书 人事-人员管理-组织架构』 发起一个组织架构调整，并提交审批后，系统会根据管理员在审批流程中配置的规则，生成 一个或多个审批单据。 |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| user_id_type | string | 否 | 用户 ID 类型 |
### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "approval_group": {
            "approval_group_id": "6991776076699549697",
            "process_id": "6991776076699549697",
            "approval_group_status": "1",
            "approval_group_status_v2": 1,
            "topic": "因组织发展需要， 变更XXX 部门组织架构",
            "adjust_reason": "例如：因业务扩展需要， 现需增设 XXX 和 XXX 两个区域部门，便于上午拓展。 ",
            "effective_date": "2022-03-01",
            "created_by": "6974641477444060708",
            "draft_id": "6991776076699549697",
            "draft_status": "Edit",
            "department_changes": [
                "7044427347159741231 "
            ],
            "job_changes": [
                "7044427347159746085"
            ],
            "position_changes": [
                "7044427347159746085"
            ]
        }
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 200 | 1162001 | Approval process not found | 请检查审批流 ID 是否正确 |
| 200 | 1161000 | Adjustment draft not found | 请确认组织架构调整记录是否存在 |

### 调用示例

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
	req := larkcorehr.NewGetApprovalGroupsReqBuilder().
		ProcessId(`6893014062142064111`).
		UserIdType(`open_id`).
		Build()

	// 发起请求
	resp, err := client.Corehr.V2.ApprovalGroups.Get(context.Background(), req)

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
    request: GetApprovalGroupsRequest = GetApprovalGroupsRequest.builder() \
        .process_id("6893014062142064111") \
        .user_id_type("open_id") \
        .build()

    # 发起请求
    response: GetApprovalGroupsResponse = client.corehr.v2.approval_groups.get(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.corehr.v2.approval_groups.get failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
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
public class GetApprovalGroupsSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      GetApprovalGroupsReq req = GetApprovalGroupsReq.newBuilder()
             .processId("6893014062142064111")
             .userIdType("open_id")
             .build();

      // 发起请求
      GetApprovalGroupsResp resp = client.corehr().v2().approvalGroups().get(req);

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

client.corehr.v2.approvalGroups.get({
        path: {
                process_id:'6893014062142064111',
        },
        params: {
                user_id_type:'open_id',
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
var client = new RestClient("https://open.feishu.cn/open-apis/corehr/v2/approval_groups/6893014062142064111?user_id_type=open_id");
client.Timeout = -1;
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "null";
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
$body = 'null';
$request = new Request('GET', 'https://open.feishu.cn/open-apis/corehr/v2/approval_groups/6893014062142064111?user_id_type=open_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X GET 'https://open.feishu.cn/open-apis/corehr/v2/approval_groups/6893014062142064111?user_id_type=open_id' \
-H 'Authorization: Bearer t-7f1b******8e560'
```

