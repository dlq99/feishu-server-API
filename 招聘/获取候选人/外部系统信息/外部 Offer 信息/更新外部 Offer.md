## 更新外部 Offer

更新外部 Offer 信息。


## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/hire/v1/external_offers/:external_offer_id` |
| HTTP Method | PUT |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom |
| 权限要求 | 更新外部 Offer |
| 权限要求 | hire:external_offer |

### 路径参数

| 参数名 | 类型 |  描述 |
| ------ | ---- | ---- |
| external_offer_id | string | 外部 Offer ID，可通过[查询外部 Offer 列表](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/external_offer/batch_query)接口获取 |

### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| external_application_id | string | 是 | 外部投递 ID，可通过[查询外部投递列表](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/external_application/list)接口获取 <br> **示例**: 7395015673275697419  |
| biz_create_time | string | 否 | Offer 创建时间，毫秒时间戳 <br> **示例**: 1721899352428  |
| owner | string | 否 | Offer 负责人姓名 <br> **示例**: 张三  |
| offer_status | string | 否 | Offer 状态 <br> **示例**: 已发送  |
| attachment_id_list | undefined[] | 否 | Offer 详情附件 ID 列表，可由[创建附件](/ssl:ttdoc/ukTMukTMukTM/uIDN1YjLyQTN24iM0UjN/create_attachment)接口返回所得 <br> **示例**:  <br> **数据校验规则**:<br>最大长度: 10最小长度: 0 |

**请求体示例**:

```json
{
    "external_application_id": "7395015673275697419",
    "biz_create_time": "1721899352428",
    "owner": "张三",
    "offer_status": "已发送",
    "attachment_id_list": [
        "7404675264888097068"
    ]
}
```

### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "SUCCESS",
    "data": {
        "external_offer": {
            "id": "6989202908470446380",
            "external_application_id": "7395015673275697419",
            "biz_create_time": "1721899352428",
            "owner": "张三",
            "offer_status": "已发送",
            "attachment_list": [
                {
                    "id": "6987954043925432620",
                    "name": "test_resume.pdf",
                    "size": 126371
                }
            ]
        }
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 500 | 1002001 | 系统异常 | 请根据实际报错信息定位问题或联系[技术支持](https://applink.feishu.cn/TLJpeNdW) |
| 400 | 1002002 | 参数错误 | 检查参数是否正确，例如类型，大小 |

### 调用示例

#### C#-restsharp

```csharp
var client = new RestClient("https://open.feishu.cn/open-apis/hire/v1/external_offers/6960663240925956660");
client.Timeout = -1;
var request = new RestRequest(Method.PUT);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"attachment_id_list\":[\"7404675264888097068\"],\"biz_create_time\":\"1721899352428\",\"external_application_id\":\"7395015673275697419\",\"offer_status\":\"已发送\",\"owner\":\"张三\"}";
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
    "external_application_id": "7395015673275697419",
    "biz_create_time": "1721899352428",
    "owner": "张三",
    "offer_status": "已发送",
    "attachment_id_list": [
        "7404675264888097068"
    ]
}';
$request = new Request('PUT', 'https://open.feishu.cn/open-apis/hire/v1/external_offers/6960663240925956660', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X PUT 'https://open.feishu.cn/open-apis/hire/v1/external_offers/6960663240925956660' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"attachment_id_list": [
		"7404675264888097068"
	],
	"biz_create_time": "1721899352428",
	"external_application_id": "7395015673275697419",
	"offer_status": "已发送",
	"owner": "张三"
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
	"github.com/larksuite/oapi-sdk-go/v3/service/hire/v1"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkhire.NewUpdateExternalOfferReqBuilder().
		ExternalOfferId(`6960663240925956660`).
		ExternalOffer(larkhire.NewExternalOfferBuilder().
			ExternalApplicationId(`7395015673275697419`).
			BizCreateTime(`1721899352428`).
			Owner(`张三`).
			OfferStatus(`已发送`).
			AttachmentIdList([]string{`7404675264888097068`}).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Hire.V1.ExternalOffer.Update(context.Background(), req)

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
from lark_oapi.api.hire.v1 import *


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
    request: UpdateExternalOfferRequest = UpdateExternalOfferRequest.builder() \
        .external_offer_id("6960663240925956660") \
        .request_body(ExternalOffer.builder()
            .external_application_id("7395015673275697419")
            .biz_create_time("1721899352428")
            .owner("张三")
            .offer_status("已发送")
            .attachment_id_list(["7404675264888097068"])
            .build()) \
        .build()

    # 发起请求
    response: UpdateExternalOfferResponse = client.hire.v1.external_offer.update(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.hire.v1.external_offer.update failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

#### Java SDK

```java
package com.lark.oapi.sample.apiall.hirev1;
import com.google.gson.JsonParser;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.hire.v1.model.*;
import java.util.HashMap;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class UpdateExternalOfferSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      UpdateExternalOfferReq req = UpdateExternalOfferReq.newBuilder()
             .externalOfferId("6960663240925956660")
             .externalOffer(ExternalOffer.newBuilder()
                 .externalApplicationId("7395015673275697419")
                 .bizCreateTime("1721899352428")
                 .owner("张三")
                 .offerStatus("已发送")
                 .attachmentIdList(new String[]{"7404675264888097068"})
                  .build())
             .build();

      // 发起请求
      UpdateExternalOfferResp resp = client.hire().v1().externalOffer().update(req);

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

client.hire.v1.externalOffer.update({
        path: {
                external_offer_id:'6960663240925956660',
        },
        data: {
                external_application_id:'7395015673275697419',
                biz_create_time:'1721899352428',
                owner:'张三',
                offer_status:'已发送',
                attachment_id_list:['7404675264888097068'],
        },
},
    lark.withTenantToken("t-7f1b******8e560")
).then(res => {
    console.log(res);
}).catch(e => {
    console.error(JSON.stringify(e.response.data, null, 4));
});

```

