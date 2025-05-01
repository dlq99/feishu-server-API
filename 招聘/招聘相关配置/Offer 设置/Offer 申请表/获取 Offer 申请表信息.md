## 获取 Offer 申请表信息

根据 Offer 申请表 ID 获取 Offer 申请表信息，可获取到的信息包括申请表名称、申请表模块、申请表字段等。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/hire/v1/offer_application_forms/:offer_application_form_id` |
| HTTP Method | GET |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 获取 offer 申请表信息 |
| 权限要求 | hire:offer_schema:readonly |

### 路径参数

| 参数名 | 类型 |  描述 |
| ------ | ---- | ---- |
| offer_application_form_id | string | Offer 申请表 ID，可通过[获取 Offer 申请表列表](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/offer_application_form/list)接口获取 |

### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "offer_apply_form": {
            "id": "7190465990618843431",
            "name": {
                "zh_cn": "校招 Offer 申请表",
                "en_us": "campus offer application form"
            },
            "schema": {
                "id": "7080465990618843430",
                "module_list": [
                    {
                        "id": "7230465990618843432",
                        "name": {
                            "zh_cn": "基础信息模块",
                            "en_us": "basic info module"
                        },
                        "is_customized": false,
                        "active_status": 1,
                        "hint": {
                            "zh_cn": "用于填写基础信息",
                            "en_us": "use for basic info"
                        },
                        "object_list": [
                            {
                                "id": "7260465990618843426",
                                "name": {
                                    "zh_cn": "薪资总包字段",
                                    "en_us": "salary total package field"
                                },
                                "description": {
                                    "zh_cn": "用于计算薪资总包",
                                    "en_us": "use for calculate salary total package"
                                },
                                "module_id": "7230465990618843432",
                                "is_customized": true,
                                "is_required": true,
                                "active_status": 1,
                                "need_approve": true,
                                "is_sensitive": false,
                                "object_type": 1,
                                "config": {
                                    "options": [
                                        {
                                            "id": "7551465990618843435",
                                            "name": {
                                                "zh_cn": "全年薪资选项",
                                                "en_us": "annual salary option"
                                            },
                                            "description": {
                                                "zh_cn": "计算全年薪资",
                                                "en_us": "calculate annual salary"
                                            }
                                        }
                                    ],
                                    "formula": {
                                        "value": "[object_id] * 12",
                                        "result": 1,
                                        "extra_map": [
                                            {
                                                "key": "object_id",
                                                "value": {
                                                    "zh_cn": "月薪",
                                                    "en_us": "monthly income"
                                                }
                                            }
                                        ]
                                    },
                                    "object_display_config": {
                                        "display_condition": 1,
                                        "pre_object_config_list": [
                                            {
                                                "id": "7560465990618843426",
                                                "operator": 1,
                                                "value": [
                                                    "1"
                                                ]
                                            }
                                        ]
                                    }
                                }
                            }
                        ]
                    }
                ]
            }
        }
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 500 | 1002001 | 系统错误 | 请根据实际报错信息定位或咨询[技术支持](https://applink.feishu.cn/TLJpeNdW) |
| 400 | 1002002 | 参数错误 | 检查参数是否正确，例如类型，大小 |

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
public class GetOfferApplicationFormSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      GetOfferApplicationFormReq req = GetOfferApplicationFormReq.newBuilder()
             .offerApplicationFormId("7680792645903286275")
             .build();

      // 发起请求
      GetOfferApplicationFormResp resp = client.hire().v1().offerApplicationForm().get(req);

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

client.hire.v1.offerApplicationForm.get({
        path: {
                offer_application_form_id:'7680792645903286275',
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
var client = new RestClient("https://open.feishu.cn/open-apis/hire/v1/offer_application_forms/7680792645903286275");
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
$request = new Request('GET', 'https://open.feishu.cn/open-apis/hire/v1/offer_application_forms/7680792645903286275', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X GET 'https://open.feishu.cn/open-apis/hire/v1/offer_application_forms/7680792645903286275' \
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
	"github.com/larksuite/oapi-sdk-go/v3/service/hire/v1"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkhire.NewGetOfferApplicationFormReqBuilder().
		OfferApplicationFormId(`7680792645903286275`).
		Build()

	// 发起请求
	resp, err := client.Hire.V1.OfferApplicationForm.Get(context.Background(), req)

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
    request: GetOfferApplicationFormRequest = GetOfferApplicationFormRequest.builder() \
        .offer_application_form_id("7680792645903286275") \
        .build()

    # 发起请求
    response: GetOfferApplicationFormResponse = client.hire.v1.offer_application_form.get(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.hire.v1.offer_application_form.get failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

