## 更新 Offer 申请表自定义字段

本接口支持修改 Offer 申请表的自定义字段，Offer 申请表的定义可参考「飞书招聘」-「设置」-「Offer 设置」-「Offer 申请表设置」中的内容。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/hire/v1/offer_custom_fields/:offer_custom_field_id` |
| HTTP Method | PUT |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom |
| 权限要求 | 更新 offer 自定义字段信息 |
| 权限要求 | hire:offer_selection_object |

### 路径参数

| 参数名 | 类型 |  描述 |
| ------ | ---- | ---- |
| offer_custom_field_id | string | Offer 申请表自定义字段 ID，可通过接口[获取 Offer 申请表信息](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/offer_application_form/get)获取 |

### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| name | object | 是 | 自定义字段名称，zh_cn和en_us必填其一 <br> **示例**:   |
| config | object | 否 | 自定义字段配置信息 <br> **示例**:   |

**类型额外说明**:

- **i18n** 类型说明:

  基本属性:

   zh_cn: string <br> en_us: string <br>
- **offer_custom_field_config** 类型说明:

  - **options** (array):
    - **offer_custom_field_config_option** 类型说明:

      - **name** (object):
        - **i18n** 类型说明:

          基本属性:

           zh_cn: string <br> en_us: string <br>


**请求体示例**:

```json
{
    "name": {
        "zh_cn": "就职状态",
        "en_us": "Employment status"
    },
    "config": {
        "options": [
            {
                "name": {
                    "zh_cn": "无业",
                    "en_us": "Unemployed"
                }
            }
        ]
    }
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
| 200 | 1002065 | 入参选项错误 | 请检查自定义字段类型，仅当自定义字段类型为「单选」或「多选」时需要传入选项信息，其余情况不传。字段类型可通过接口[获取 Offer 申请表信息](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/offer_application_form/get)获取 |

### 调用示例

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
    request: UpdateOfferCustomFieldRequest = UpdateOfferCustomFieldRequest.builder() \
        .offer_custom_field_id("6906755946257615112") \
        .request_body(OfferCustomField.builder()
            .name(I18n.builder()
                .zh_cn("就职状态")
                .en_us("Employment status")
                .build())
            .config(OfferCustomFieldConfig.builder()
                .options([OfferCustomFieldConfigOption.builder()
                    .name(I18n.builder()
                        .zh_cn("无业")
                        .en_us("Unemployed")
                        .build())
                    .build()
                    ])
                .build())
            .build()) \
        .build()

    # 发起请求
    response: UpdateOfferCustomFieldResponse = client.hire.v1.offer_custom_field.update(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.hire.v1.offer_custom_field.update failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
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
public class UpdateOfferCustomFieldSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      UpdateOfferCustomFieldReq req = UpdateOfferCustomFieldReq.newBuilder()
             .offerCustomFieldId("6906755946257615112")
             .offerCustomField(OfferCustomField.newBuilder()
                 .name(I18n.newBuilder()
                        .zhCn("就职状态")
                        .enUs("Employment status")
                        .build())
                 .config(OfferCustomFieldConfig.newBuilder()
                        .options(new OfferCustomFieldConfigOption[]{
                        OfferCustomFieldConfigOption.newBuilder()
                          .name(I18n.newBuilder()
                            .zhCn("无业")
                            .enUs("Unemployed")
                            .build())
                          .build()
                        })
                        .build())
                  .build())
             .build();

      // 发起请求
      UpdateOfferCustomFieldResp resp = client.hire().v1().offerCustomField().update(req);

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

client.hire.v1.offerCustomField.update({
        path: {
                offer_custom_field_id:'6906755946257615112',
        },
        data: {
                name:{
                        zh_cn:'就职状态',
                        en_us:'Employment status',
                        },
                config:{
                        options:[
                        {
                          name:{
                            zh_cn:'无业',
                            en_us:'Unemployed',
                            },
                          }
                        ],
                        },
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
var client = new RestClient("https://open.feishu.cn/open-apis/hire/v1/offer_custom_fields/6906755946257615112");
client.Timeout = -1;
var request = new RestRequest(Method.PUT);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"config\":{\"options\":[{\"name\":{\"en_us\":\"Unemployed\",\"zh_cn\":\"无业\"}}]},\"name\":{\"en_us\":\"Employment status\",\"zh_cn\":\"就职状态\"}}";
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
    "name": {
        "zh_cn": "就职状态",
        "en_us": "Employment status"
    },
    "config": {
        "options": [
            {
                "name": {
                    "zh_cn": "无业",
                    "en_us": "Unemployed"
                }
            }
        ]
    }
}';
$request = new Request('PUT', 'https://open.feishu.cn/open-apis/hire/v1/offer_custom_fields/6906755946257615112', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X PUT 'https://open.feishu.cn/open-apis/hire/v1/offer_custom_fields/6906755946257615112' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"config": {
		"options": [
			{
				"name": {
					"en_us": "Unemployed",
					"zh_cn": "无业"
				}
			}
		]
	},
	"name": {
		"en_us": "Employment status",
		"zh_cn": "就职状态"
	}
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
	req := larkhire.NewUpdateOfferCustomFieldReqBuilder().
		OfferCustomFieldId(`6906755946257615112`).
		OfferCustomField(larkhire.NewOfferCustomFieldBuilder().
			Name(larkhire.NewI18nBuilder().
				ZhCn(`就职状态`).
				EnUs(`Employment status`).
				Build()).
			Config(larkhire.NewOfferCustomFieldConfigBuilder().
				Options([]*larkhire.OfferCustomFieldConfigOption{
					larkhire.NewOfferCustomFieldConfigOptionBuilder().
						Name(larkhire.NewI18nBuilder().
							ZhCn(`无业`).
							EnUs(`Unemployed`).
							Build()).
						Build(),
				}).
				Build()).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Hire.V1.OfferCustomField.Update(context.Background(), req)

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

