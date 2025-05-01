## 获取 Offer 信息

根据投递 ID 获取 Offer 信息。

💡 
 注意：该接口暂时不支持查询实习Offer

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/hire/v1/applications/:application_id/offer` |
| HTTP Method | GET |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 更新投递信息 <br> 获取用户 user ID <br> 获取投递信息 |
| 权限要求 | hire:application:readonly <br> hire:application |

### 路径参数

| 参数名 | 类型 |  描述 |
| ------ | ---- | ---- |
| application_id | string | 投递ID，可通过[获取投递列表](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/application/list)获取 |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| user_id_type | string | 否 | 用户 ID 类型 |
| department_id_type | string | 否 | 此次调用中使用的部门 ID 类型。 |
| job_level_id_type | string | 否 | 此次调用中使用的「职级 ID」的类型 |
| job_family_id_type | string | 否 | 此次调用中使用的「序列 ID」的类型 |
| employee_type_id_type | string | 否 | 此次调用中使用的「人员类型 ID」的类型 |
### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "ok",
    "data": {
        "offer": {
            "id": "7057802493489285412",
            "application_id": "7020661401874614564",
            "basic_info": {
                "offer_type": 1,
                "remark": "10",
                "expire_time": 1653383498000,
                "owner_user_id": "ou_99be8e24ad1ad390b6cd3b8916940df1",
                "creator_user_id": "ou_99be8e24ad1ad390b6cd3b8916940df1",
                "employee_type": {
                    "id": "1",
                    "zh_name": "正式",
                    "en_name": "Regular"
                },
                "create_time": "1628512038000",
                "leader_user_id": "ou_99be8e24ad1ad390b6cd3b8916940df1",
                "onboard_date": "2021-05-20",
                "department_id": "od-6b394871807047c7023ebfc1ff37cd3a",
                "probation_month": 1,
                "contract_year": 3,
                "contract_period": {
                    "period_type": 1,
                    "period": 3
                },
                "recruitment_type": {
                    "id": "1",
                    "zh_name": "正式",
                    "en_name": "Regular"
                },
                "sequence": {
                    "id": "1",
                    "zh_name": "正式",
                    "en_name": "Regular"
                },
                "level": {
                    "id": "1",
                    "zh_name": "正式",
                    "en_name": "Regular"
                },
                "onboard_address": {
                    "id": "6932753007915206919",
                    "zh_name": "名字",
                    "en_name": "name",
                    "district": {
                        "zh_name": "伦敦",
                        "en_name": "London",
                        "code": "400700",
                        "location_type": 1
                    },
                    "city": {
                        "zh_name": "中文",
                        "en_name": "eng",
                        "code": "400700",
                        "location_type": 1
                    },
                    "state": {
                        "zh_name": "中文",
                        "en_name": "eng",
                        "code": "400700",
                        "location_type": 1
                    },
                    "country": {
                        "zh_name": "中文",
                        "en_name": "eng",
                        "code": "400700",
                        "location_type": 1
                    }
                },
                "work_address": {
                    "id": "6932753007915206919",
                    "zh_name": "名字",
                    "en_name": "name",
                    "district": {
                        "zh_name": "伦敦",
                        "en_name": "London",
                        "code": "400700",
                        "location_type": 1
                    },
                    "city": {
                        "zh_name": "中文",
                        "en_name": "eng",
                        "code": "400700",
                        "location_type": 1
                    },
                    "state": {
                        "zh_name": "中文",
                        "en_name": "eng",
                        "code": "400700",
                        "location_type": 1
                    },
                    "country": {
                        "zh_name": "中文",
                        "en_name": "eng",
                        "code": "400700",
                        "location_type": 1
                    }
                },
                "customize_info_list": [
                    {
                        "object_id": "key",
                        "customize_value": "value"
                    }
                ],
                "position_id": "123",
                "job_offered": "入职职位",
                "job_grade_id": "6897079709306259720",
                "common_attachment_id_list": [
                    "7483412052430997804"
                ]
            },
            "salary_plan": {
                "currency": "CNY",
                "basic_salary": "{\"amount\":\"10000\",\"period\":2}",
                "probation_salary_percentage": "10%",
                "award_salary_multiple": "12",
                "option_shares": "11",
                "quarterly_bonus": "11111",
                "half_year_bonus": "11111",
                "total_annual_cash": "11111",
                "customize_info_list": [
                    {
                        "object_id": "key",
                        "customize_value": "value"
                    }
                ]
            },
            "schema_id": "6963562624677398823",
            "offer_status": 0,
            "job_info": {
                "job_id": "7080891505426925854",
                "job_name": "xx"
            },
            "customized_module_list": [
                {
                    "ID": "6930815272790114324",
                    "object_list": [
                        {
                            "object_id": "6930815272790114324",
                            "customize_value": "value"
                        }
                    ]
                }
            ],
            "job_requirement_id": "1231231232312312",
            "offer_send_record_list": [
                {
                    "offer_send_record_id": "1718959426734",
                    "operator_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
                    "send_time": "1718959426734",
                    "offer_letter_status": 1,
                    "email_info": {
                        "cc_email_list": [
                            "123@test.com"
                        ],
                        "receiver_email_list": [
                            "123@test.com"
                        ],
                        "content": "This is a test email."
                    },
                    "acceptance_list": [
                        {
                            "operator_type": 1,
                            "conclusion": 1,
                            "memo": "Abort",
                            "operate_time": "1718959426734"
                        }
                    ],
                    "offer_file_list": [
                        {
                            "id": "12345678901",
                            "file_template_id": "1718959426734",
                            "file_template_name": "offer 文件",
                            "file_template_type_id": "1718959426734",
                            "file_template_type_name": "offer 文件"
                        }
                    ],
                    "offer_signature_info": {
                        "id": "1718959426734",
                        "signature_status": 1,
                        "attachment_list": [
                            {
                                "id": "12345678901",
                                "file_name": "offer 文件",
                                "file_template_id": "1718959426734",
                                "file_template_name": "offer 文件",
                                "file_template_type_id": "1718959426734",
                                "file_template_type_name": "offer 文件"
                            }
                        ]
                    }
                }
            ]
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
client.request({
    url: '/open-apis/hire/v1/applications/6949805467799537964/offer?department_id_type=%22open_department_id%22&employee_type_id_type=%22people_admin_employee_type_id%22&job_family_id_type=%22people_admin_job_category_id%22&job_level_id_type=%22people_admin_job_level_id%22&user_id_type=open_id',
    method: 'GET',
            data: null,
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
var client = new RestClient("https://open.feishu.cn/open-apis/hire/v1/applications/6949805467799537964/offer?department_id_type=%22open_department_id%22&employee_type_id_type=%22people_admin_employee_type_id%22&job_family_id_type=%22people_admin_job_category_id%22&job_level_id_type=%22people_admin_job_level_id%22&user_id_type=open_id");
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
$request = new Request('GET', 'https://open.feishu.cn/open-apis/hire/v1/applications/6949805467799537964/offer?department_id_type=%22open_department_id%22&employee_type_id_type=%22people_admin_employee_type_id%22&job_family_id_type=%22people_admin_job_category_id%22&job_level_id_type=%22people_admin_job_level_id%22&user_id_type=open_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X GET 'https://open.feishu.cn/open-apis/hire/v1/applications/6949805467799537964/offer?department_id_type=%22open_department_id%22&employee_type_id_type=%22people_admin_employee_type_id%22&job_family_id_type=%22people_admin_job_category_id%22&job_level_id_type=%22people_admin_job_level_id%22&user_id_type=open_id' \
-H 'Authorization: Bearer t-7f1b******8e560'
```

#### Golang SDK

```go
package main

import (
	"context"
	"encoding/json"
	"fmt"
	"github.com/larksuite/oapi-sdk-go/v3"
	"github.com/larksuite/oapi-sdk-go/v3/core"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求体
	bodyJsonStr := `null`
	body := map[string]interface{}{}
	err := json.Unmarshal([]byte(bodyJsonStr), &body)
	if err != nil {
		fmt.Println(err)
		return
	}

	// 发起请求
	resp, err := client.Get(context.Background(),
		"/open-apis/hire/v1/applications/6949805467799537964/offer?department_id_type=%22open_department_id%22&employee_type_id_type=%22people_admin_employee_type_id%22&job_family_id_type=%22people_admin_job_category_id%22&job_level_id_type=%22people_admin_job_level_id%22&user_id_type=open_id",
		body,
		larkcore.AccessTokenTypeTenant)

	// 错误处理
	if err != nil {
		fmt.Println(err)
		return
	}

	// 获取请求 ID
	fmt.Println(resp.RequestId())

	// 处理请求结果
	fmt.Println(resp.StatusCode)      // http status code
	fmt.Println(resp.Header)          // http header
	fmt.Println(string(resp.RawBody)) // http body
}

```

#### Python SDK

```python
import json

import lark_oapi as lark
import json
from requests_toolbelt import MultipartEncoder


# SDK 使用说明: https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/python--sdk/preparations-before-development
# 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
def main():
    # 创建client
    client = lark.Client.builder() \
        .app_id("YOUR_APP_ID") \
        .app_secret("YOUR_APP_SECRET") \
        .log_level(lark.LogLevel.DEBUG) \
        .build()

    # 构造请求对象
    json_str = "null"
    body = json.loads(json_str)
    request: lark.BaseRequest = lark.BaseRequest.builder() \
        .http_method(lark.HttpMethod.GET) \
        .uri("/open-apis/hire/v1/applications/6949805467799537964/offer?department_id_type=%22open_department_id%22&employee_type_id_type=%22people_admin_employee_type_id%22&job_family_id_type=%22people_admin_job_category_id%22&job_level_id_type=%22people_admin_job_level_id%22&user_id_type=open_id") \
        .token_types({lark.AccessTokenType.TENANT}) \
        .body(body) \
        .build()

    # 发起请求
    response: lark.BaseResponse = client.request(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.request failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(str(response.raw.content, lark.UTF_8))


if __name__ == "__main__":
    main()

```

#### Java SDK

```java
package com.lark.oapi.sample.apiall.hirev1;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import java.util.Map;
import com.lark.oapi.core.response.RawResponse;
import com.lark.oapi.core.token.AccessTokenType;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class OfferApplicationSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      String bodyJsonStr = "null";
      Map<String, Object> body = Jsons.DEFAULT.fromJson(bodyJsonStr, Map.class);

      // 发起请求
      RawResponse resp = client.get(
         "/open-apis/hire/v1/applications/6949805467799537964/offer?department_id_type=%22open_department_id%22&employee_type_id_type=%22people_admin_employee_type_id%22&job_family_id_type=%22people_admin_job_category_id%22&job_level_id_type=%22people_admin_job_level_id%22&user_id_type=open_id"
		 ,body
         ,AccessTokenType.Tenant);

      // 业务数据处理
      System.out.println(resp.getStatusCode());
      System.out.println(Jsons.DEFAULT.toJson(resp.getHeaders()));
      System.out.println(new String(resp.getBody()));
      System.out.println(resp.getRequestID());
 }
}

```

