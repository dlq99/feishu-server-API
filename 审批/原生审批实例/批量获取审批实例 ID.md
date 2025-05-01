## 批量获取审批实例 ID

根据审批定义的 approval_code 批量获取审批实例的 instance_code，用于拉取企业下某个审批定义的全部审批实例。默认以审批创建时间先后顺序排列。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/approval/v4/instances` |
| HTTP Method | GET |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 查看、创建、更新、删除原生审批实例相关信息 <br> 查看、创建、更新、删除审批应用相关信息 <br> 访问审批应用 |
| 权限要求 | approval:approval <br> approval:approval:readonly <br> approval:instance |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| page_size | integer | 否 | 分页大小，用于指定一次请求所返回的数据量上限。 |
| page_token | string | 否 | 分页标记，第一次请求不填，表示从头开始遍历；分页查询结果还有更多项时会同时返回新的 page_token，下次遍历可采用该 page_token 获取查询结果 |
| approval_code | string | 是 | 审批定义 Code。获取方式：

- 调用[创建审批定义](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/approval-v4/approval/create)接口后，从响应参数 approval_code 获取。
- 登录审批管理后台，在指定审批定义的 URL 中获取，具体操作参见[什么是 Approval Code](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/approval-v4/approval/overview-of-approval-resources#8151e0ae)。 |
| start_time | string | 是 | 审批实例创建时间的开始区间，毫秒时间戳。

**说明**：start_time 与 end_time 组成时间区间查询条件，接口会返回在该时间区间内创建的审批实例数据。 |
| end_time | string | 是 | 审批实例创建时间的结束区间，毫秒时间戳。

**说明**：start_time 与 end_time 组成时间区间查询条件，接口会返回在该时间区间内创建的审批实例的 Code。 |
### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "instance_code_list": [
            "357C21A0-2069-4F6B-955F-1DFBE6710C51"
        ],
        "page_token": "nF1ZXJ5VGhlbkZldGNoCgAAAAAA6PZwFmUzSldvTC1yU",
        "has_more": false
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 400 | 1390001 | param is invalid | 参数错误。排查方案：<br><br>- 根据接口文档的参数说明，检查请求时传入的参数是否正确。<br><br>- 如果传入的有表单参数（form），则需要检查该参数内传入的表单控件数据是否正确。如果报错信息内包含控件 ID（如 `控件= widget17261088448220001`），可以调用[查看指定审批定义](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/approval-v4/approval/get)或者[获取单个审批实例详情](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/approval-v4/instance/get)接口，获取响应参数 form 值，检索有问题的控件 ID，然后检查该控件的配置是否正确。 |
| 400 | 1390002 | approval code not found | 找不到审批定义 Code，检查传入的审批定义 Code 是否正确。<br><br>审批定义 Code 获取方式：<br><br>- 调用[创建审批定义](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/approval-v4/approval/create)接口后，从响应参数 approval_code 获取。<br>- 登录审批管理后台，在指定审批定义的 URL 中获取，具体操作参见[什么是 Approval Code](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/approval-v4/approval/overview-of-approval-resources#8151e0ae)。 |
| 400 | 1395001 | There have been some errors. Please try again later | 服务出现错误。排查方案：<br><br>1. 参考接口文档的参数说明，检查请求时传入的参数是否正确。如果传入的有表单参数（form），则需要检查传入的表单控件数据是否正确。<br><br>2. 降低请求频率，并重试。如果重试仍然报错，请联系[技术支持](https://applink.feishu.cn/TLJpeNdW)。 |

### 调用示例

#### Python SDK

```python
import json

import lark_oapi as lark
from lark_oapi.api.approval.v4 import *


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
    request: ListInstanceRequest = ListInstanceRequest.builder() \
        .page_size(100) \
        .page_token("nF1ZXJ5VGhlbkZldGNoCgAAAAAA6PZwFmUzSldvTC1yU") \
        .approval_code("7C468A54-8745-2245-9675-08B7C63E7A85") \
        .start_time("1567690398020") \
        .end_time("1567690398020") \
        .build()

    # 发起请求
    response: ListInstanceResponse = client.approval.v4.instance.list(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.approval.v4.instance.list failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

#### Java SDK

```java
package com.lark.oapi.sample.apiall.approvalv4;
import com.google.gson.JsonParser;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.approval.v4.model.*;
import java.util.HashMap;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class ListInstanceSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      ListInstanceReq req = ListInstanceReq.newBuilder()
             .pageSize(100)
             .pageToken("nF1ZXJ5VGhlbkZldGNoCgAAAAAA6PZwFmUzSldvTC1yU")
             .approvalCode("7C468A54-8745-2245-9675-08B7C63E7A85")
             .startTime("1567690398020")
             .endTime("1567690398020")
             .build();

      // 发起请求
      ListInstanceResp resp = client.approval().v4().instance().list(req);

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

client.approval.v4.instance.list({
        params: {
                page_size:100,
                page_token:'nF1ZXJ5VGhlbkZldGNoCgAAAAAA6PZwFmUzSldvTC1yU',
                approval_code:'7C468A54-8745-2245-9675-08B7C63E7A85',
                start_time:'1567690398020',
                end_time:'1567690398020',
        },
},
    lark.withTenantToken("t-7f1b******8e560")
).then(res => {
    console.log(res);
}).catch(e => {
    console.error(JSON.stringify(e.response.data, null, 4));
});

// 还可以使用迭代器的方式便捷的获取数据，无需手动维护page_token
(async () => {
    for await (const item of await client.approval.v4.instance.listWithIterator({
            params: {
                        page_size:100,
                        approval_code:'7C468A54-8745-2245-9675-08B7C63E7A85',
                        start_time:'1567690398020',
                        end_time:'1567690398020',
            },
    },
        lark.withTenantToken("t-7f1b******8e560")
    )) {
        console.log(item);
    }
})();
```

#### C#-restsharp

```csharp
var client = new RestClient("https://open.feishu.cn/open-apis/approval/v4/instances?approval_code=7C468A54-8745-2245-9675-08B7C63E7A85&end_time=1567690398020&page_size=100&page_token=nF1ZXJ5VGhlbkZldGNoCgAAAAAA6PZwFmUzSldvTC1yU&start_time=1567690398020");
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
$request = new Request('GET', 'https://open.feishu.cn/open-apis/approval/v4/instances?approval_code=7C468A54-8745-2245-9675-08B7C63E7A85&end_time=1567690398020&page_size=100&page_token=nF1ZXJ5VGhlbkZldGNoCgAAAAAA6PZwFmUzSldvTC1yU&start_time=1567690398020', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X GET 'https://open.feishu.cn/open-apis/approval/v4/instances?approval_code=7C468A54-8745-2245-9675-08B7C63E7A85&end_time=1567690398020&page_size=100&page_token=nF1ZXJ5VGhlbkZldGNoCgAAAAAA6PZwFmUzSldvTC1yU&start_time=1567690398020' \
-H 'Authorization: Bearer t-7f1b******8e560'
```

#### Golang SDK

```go
package main

import (
	"context"
	"fmt"
	"github.com/larksuite/oapi-sdk-go/v3"
	"github.com/larksuite/oapi-sdk-go/v3/core"
	"github.com/larksuite/oapi-sdk-go/v3/service/approval/v4"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkapproval.NewListInstanceReqBuilder().
		PageSize(100).
		PageToken(`nF1ZXJ5VGhlbkZldGNoCgAAAAAA6PZwFmUzSldvTC1yU`).
		ApprovalCode(`7C468A54-8745-2245-9675-08B7C63E7A85`).
		StartTime(`1567690398020`).
		EndTime(`1567690398020`).
		Build()

	// 发起请求
	resp, err := client.Approval.V4.Instance.List(context.Background(), req)

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

