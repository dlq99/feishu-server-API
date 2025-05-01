## 批量获取 OKR

根据 OKR id 批量获取 OKR。

💡 
 使用<md-tag mode="inline" type="token-tenant">tenant_access_token</md-tag>需要额外申请权限<md-perm 
href="/ssl:ttdoc/ukTMukTMukTM/uQjN3QjL0YzN04CN2cDN">以应用身份访问OKR信息</md-perm>

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/okr/v1/okrs/batch_get` |
| HTTP Method | GET |
| 支持的访问令牌 | tenant_access_token, user_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 更新 OKR 信息 <br> 获取用户 user ID <br> 获取 OKR 信息 |
| 权限要求 | okr:okr:readonly <br> okr:okr |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| user_id_type | string | 否 | 用户 ID 类型 |
| okr_ids | array | 是 | OKR ID 列表，最多10个 |
| lang | string | 否 | 请求OKR的语言版本（比如@的人名），lang=en_us/zh_cn，请求 Query中 |
### 响应

**响应示例**:

```json
{
    "code": 0,
    "data": {
        "okr_list": [
            {
                "confirm_status": 4,
                "id": "7072252816005349396",
                "name": "2022 年 3 月",
                "objective_list": [
                    {
                        "aligned_objective_list": [],
                        "aligning_objective_list": [],
                        "content": "需求@刘三",
                        "deadline": "1648656000000",
                        "id": "7073360513731690515",
                        "kr_list": [
                            {
                                "content": "1111@张三9",
                                "deadline": "1648656000000",
                                "id": "7073360471990140948",
                                "kr_weight": 50,
                                "mentioned_user_list": [
                                    {
                                        "open_id": "ou_a79faffdb6aee3618f0da4d42b192466",
                                        "user_id": "ou_a79faffdb6aee3618f0da4d42b192466"
                                    }
                                ],
                                "progress_rate": {
                                    "percent": 60,
                                    "status": "1"
                                },
                                "progress_rate_percent_last_updated_time": "1646907176099",
                                "progress_rate_status_last_updated_time": "1646907176099",
                                "progress_record_last_updated_time": "1646907586253",
                                "progress_record_list": [
                                    {
                                        "id": "7073411057431199764"
                                    },
                                    {
                                        "id": "7073410950174392340"
                                    },
                                    {
                                        "id": "7073360480580010004"
                                    },
                                    {
                                        "id": "7073360513731805203"
                                    }
                                ],
                                "progress_report_last_updated_time": "0",
                                "score": 100,
                                "score_last_updated_time": "1646907586244",
                                "weight": 50
                            }
                        ],
                        "mentioned_user_list": [
                            {
                                "open_id": "ou_ab08720df94e64045cc8c2b7694ef2a0",
                                "user_id": "ou_ab08720df94e64045cc8c2b7694ef2a0"
                            }
                        ],
                        "permission": 1,
                        "progress_rate": {
                            "percent": 30,
                            "status": "0"
                        },
                        "progress_rate_percent_last_updated_time": "1646907261326",
                        "progress_rate_status_last_updated_time": "1646907261326",
                        "progress_record_last_updated_time": "1646907590448",
                        "progress_record_list": [
                            {
                                "id": "7073410950447120403"
                            },
                            {
                                "id": "7073410950174474260"
                            },
                            {
                                "id": "7073360502990094355"
                            },
                            {
                                "id": "7073360502990061587"
                            }
                        ],
                        "progress_report": "红豆泥",
                        "progress_report_last_updated_time": "1646907387911",
                        "score": 100,
                        "score_last_updated_time": "1646907590472",
                        "weight": 40
                    }
                ],
                "period_id": "7067724095781142548",
                "permission": 1
            }
        ]
    },
    "msg": "success"
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 500 | 1009999 | Unknown error. Please contact Feishu Assistant or your customer success manager. | 内部错误，请联系飞书助手或您的客户成功经理 |
| 500 | 1009998 | system exception | 系统异常 |
| 400 | 1001001 | Invalid parameters. Please check document and modify accordingly. | 无效的参数，请对照文档检查输入的参数 |
| 400 | 1001002 | No permission. | 您无权访问该接口，请确认您的登录凭证 |
| 400 | 1001003 | User not found. | 用户不存在 |
| 400 | 1001004 | OKR data not found. | 对应ID的数据不存在 |

### 调用示例

#### Golang SDK

```go
package main

import (
	"context"
	"fmt"
	"github.com/larksuite/oapi-sdk-go/v3"
	"github.com/larksuite/oapi-sdk-go/v3/core"
	"github.com/larksuite/oapi-sdk-go/v3/service/okr/v1"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkokr.NewBatchGetOkrReqBuilder().
		UserIdType(`open_id`).
		OkrIds(7043693679567028244).
		Lang(`zh_cn`).
		Build()

	// 发起请求
	resp, err := client.Okr.V1.Okr.BatchGet(context.Background(), req)

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
from lark_oapi.api.okr.v1 import *


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
    request: BatchGetOkrRequest = BatchGetOkrRequest.builder() \
        .user_id_type("open_id") \
        .okr_ids(7043693679567028244) \
        .lang("zh_cn") \
        .build()

    # 发起请求
    response: BatchGetOkrResponse = client.okr.v1.okr.batch_get(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.okr.v1.okr.batch_get failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

#### Java SDK

```java
package com.lark.oapi.sample.apiall.okrv1;
import com.google.gson.JsonParser;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.okr.v1.model.*;
import java.util.HashMap;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class BatchGetOkrSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      BatchGetOkrReq req = BatchGetOkrReq.newBuilder()
             .userIdType("open_id")
             .okrIds(7043693679567028244)
             .lang("zh_cn")
             .build();

      // 发起请求
      BatchGetOkrResp resp = client.okr().v1().okr().batchGet(req);

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

client.okr.v1.okr.batchGet({
        params: {
                user_id_type:'open_id',
                okr_ids:7043693679567028244,
                lang:'zh_cn',
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
var client = new RestClient("https://open.feishu.cn/open-apis/okr/v1/okrs/batch_get?lang=zh_cn&okr_ids=7043693679567028244&user_id_type=open_id");
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
$request = new Request('GET', 'https://open.feishu.cn/open-apis/okr/v1/okrs/batch_get?lang=zh_cn&okr_ids=7043693679567028244&user_id_type=open_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X GET 'https://open.feishu.cn/open-apis/okr/v1/okrs/batch_get?lang=zh_cn&okr_ids=7043693679567028244&user_id_type=open_id' \
-H 'Authorization: Bearer t-7f1b******8e560'
```

