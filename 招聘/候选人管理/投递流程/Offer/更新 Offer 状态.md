## 更新 Offer 状态

通过 Offer ID 更新候选人 Offer 的「Offer 审批状态」或 「Offer 发送和接受状态」。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/hire/v1/offers/:offer_id/offer_status` |
| HTTP Method | PATCH |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom |
| 权限要求 | 更新 offer 信息 |
| 权限要求 | hire:offer |

### 路径参数

| 参数名 | 类型 |  描述 |
| ------ | ---- | ---- |
| offer_id | string | Offer ID，如何获取请参考[获取 Offer 列表](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/offer/list) |

### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| offer_status | integer | 是 | Offer 状态 <br> **示例**: 6 <br> **可选值**:<br>- 2: Offer 审批中 <br>- 3: Offer 审批已撤回 <br>- 4: Offer 审批通过 <br>- 5: Offer 审批不通过 <br>- 6: Offer 已发送 <br>- 7: Offer 被候选人接受 <br>- 8: Offer 被候选人拒绝 <br>- 9: Offer 已失效 <br>- 10: Offer 已创建 <br> |
| expiration_date | string | 否 | Offer 失效时间<br><br><br><br>**注意**：当请求参数 offer_status 为「Offer 已发送」时必填<br><br><br><br>**值格式**："YYYY-MM-DD" <br> **示例**: 2023-01-01  |
| termination_reason_id_list | undefined[] | 否 | 终止原因 ID 列表，可通过[获取终止投递原因](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/termination_reason/list)接口获取<br><br><br><br>**最大长度**：<br>50<br><br><br><br>**注意**：当请求参数 offer_status 为「Offer 被候选人拒绝」时必填 <br> **示例**:   |
| termination_reason_note | string | 否 | Offer 终止备注信息 <br> **示例**: 不符合期望  |

**请求体示例**:

```json
{
    "offer_status": 6,
    "expiration_date": "2023-01-01",
    "termination_reason_id_list": [
        "6891560630172518670"
    ],
    "termination_reason_note": "不符合期望"
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
| 500 | 1002001 | 系统错误 | 请根据实际报错信息定位或咨询[技术支持](https://applink.feishu.cn/TLJpeNdW) |
| 400 | 1002002 | 参数错误 | 检查参数是否正确，例如类型，大小 |
| 400 | 1002064 | Offer 不存在 | Offer ID 非法，请检查入参 `offer_id` 是否正确 |
| 500 | 1002069 | Offer 审批状态更新失败 | 确认 Offer 当前状态，更新 Offer 审批状态需遵循状态流转规则 |
| 400 | 1002070 | 当前 Offer 已通过飞书招聘发起过审批，不可再通过此接口更新 Offer 状态 | 确认 Offer 是否已由飞书招聘系统发起审批 |
| 400 | 1002071 | 当前投递阶段不可更新Offer 接受状态 | 确认当前投递阶段是否在「待入职」之前 |
| 400 | 1002072 | 不可将 Offer 置为已失效 | 确认当前 Offer 的状态为「已发出」或「候选人已接受」 |
| 500 | 1002073 | 当前 Offer 已通过飞书招聘发送给候选人，不可通过该接口更新 Offer 发送和接受状态 | 确实当前 Offer 是否已经在飞书招聘系统发送给候选人 |
| 500 | 1002074 | 同步开关尚未打开，仅支持在招聘系统中创建 <br> Offer、修改 Offer 状态和发送 Offer | 请前往「飞书招聘」-「设置」-「Offer 设置」-「Offer 规则设置」开启对应开关 |

### 调用示例

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
public class OfferStatusOfferSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      OfferStatusOfferReq req = OfferStatusOfferReq.newBuilder()
             .offerId("6930815272790114324")
             .offerStatusOfferReqBody(OfferStatusOfferReqBody.newBuilder()
                 .offerStatus(6)
                 .expirationDate("2023-01-01")
                 .terminationReasonIdList(new String[]{"6891560630172518670"})
                 .terminationReasonNote("不符合期望")
                  .build())
             .build();

      // 发起请求
      OfferStatusOfferResp resp = client.hire().v1().offer().offerStatus(req);

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

client.hire.v1.offer.offerStatus({
        path: {
                offer_id:'6930815272790114324',
        },
        data: {
                offer_status:6,
                expiration_date:'2023-01-01',
                termination_reason_id_list:['6891560630172518670'],
                termination_reason_note:'不符合期望',
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
var client = new RestClient("https://open.feishu.cn/open-apis/hire/v1/offers/6930815272790114324/offer_status");
client.Timeout = -1;
var request = new RestRequest(Method.PATCH);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"expiration_date\":\"2023-01-01\",\"offer_status\":6,\"termination_reason_id_list\":[\"6891560630172518670\"],\"termination_reason_note\":\"不符合期望\"}";
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
    "offer_status": 6,
    "expiration_date": "2023-01-01",
    "termination_reason_id_list": [
        "6891560630172518670"
    ],
    "termination_reason_note": "不符合期望"
}';
$request = new Request('PATCH', 'https://open.feishu.cn/open-apis/hire/v1/offers/6930815272790114324/offer_status', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X PATCH 'https://open.feishu.cn/open-apis/hire/v1/offers/6930815272790114324/offer_status' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"expiration_date": "2023-01-01",
	"offer_status": 6,
	"termination_reason_id_list": [
		"6891560630172518670"
	],
	"termination_reason_note": "不符合期望"
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
	req := larkhire.NewOfferStatusOfferReqBuilder().
		OfferId(`6930815272790114324`).
		Body(larkhire.NewOfferStatusOfferReqBodyBuilder().
			OfferStatus(6).
			ExpirationDate(`2023-01-01`).
			TerminationReasonIdList([]string{`6891560630172518670`}).
			TerminationReasonNote(`不符合期望`).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Hire.V1.Offer.OfferStatus(context.Background(), req)

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
    request: OfferStatusOfferRequest = OfferStatusOfferRequest.builder() \
        .offer_id("6930815272790114324") \
        .request_body(OfferStatusOfferRequestBody.builder()
            .offer_status(6)
            .expiration_date("2023-01-01")
            .termination_reason_id_list(["6891560630172518670"])
            .termination_reason_note("不符合期望")
            .build()) \
        .build()

    # 发起请求
    response: OfferStatusOfferResponse = client.hire.v1.offer.offer_status(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.hire.v1.offer.offer_status failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

