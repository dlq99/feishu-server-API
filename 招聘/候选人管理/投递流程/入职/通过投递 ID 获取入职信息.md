## 通过投递 ID 获取入职信息

通过投递 ID 获取员工入职信息。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/hire/v1/employees/get_by_application` |
| HTTP Method | GET |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 获取招聘员工信息 <br> 更新招聘员工信息 <br> 获取用户 user ID |
| 权限要求 | hire:employee:readonly <br> hire:employee |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| application_id | string | 是 | 投递ID，可通过[获取投递列表](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/application/list)接口获取 |
| user_id_type | string | 否 | 用户 ID 类型 |
| department_id_type | string | 否 | 指定查询结果中的部门 ID 类型。关于部门 ID 的详细介绍，可参见[部门资源介绍](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview)。
 |
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
        "employee": {
            "id": "7095600054216542508",
            "application_id": "7073372582620416300",
            "onboard_status": 1,
            "conversion_status": 1,
            "onboard_time": 1637596800000,
            "expected_conversion_time": 1637596800000,
            "actual_conversion_time": 1637596800000,
            "overboard_time": 1637596800000,
            "overboard_note": "职业发展考虑",
            "onboard_city_code": "CT_2",
            "department": "6966123381141866028",
            "leader": "ou-xxx",
            "sequence": "6937934036379650311",
            "level": "7006234385490345986",
            "employee_type": "1",
            "job_requirement_id": "123123123213"
        }
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 500 | 1002001 | 系统错误 | 请根据实际报错信息定位或咨询[技术支持](https://applink.feishu.cn/TLJpeNdW) |
| 400 | 1002002 | 参数错误 | 检查参数是否正确，例如类型，大小 |
| 400 | 1002903 | 员工不存在 | 请确认入参 `employee_id` 是否正确 |

### 调用示例

#### C#-restsharp

```csharp
var client = new RestClient("https://open.feishu.cn/open-apis/hire/v1/employees/get_by_application?application_id=7379910335417927975&department_id_type=%22department_id%22&employee_type_id_type=%22people_admin_employee_type_id%22&job_family_id_type=%22people_admin_job_category_id%22&job_level_id_type=%22people_admin_job_level_id%22&user_id_type=open_id");
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
$request = new Request('GET', 'https://open.feishu.cn/open-apis/hire/v1/employees/get_by_application?application_id=7379910335417927975&department_id_type=%22department_id%22&employee_type_id_type=%22people_admin_employee_type_id%22&job_family_id_type=%22people_admin_job_category_id%22&job_level_id_type=%22people_admin_job_level_id%22&user_id_type=open_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X GET 'https://open.feishu.cn/open-apis/hire/v1/employees/get_by_application?application_id=7379910335417927975&department_id_type=%22department_id%22&employee_type_id_type=%22people_admin_employee_type_id%22&job_family_id_type=%22people_admin_job_category_id%22&job_level_id_type=%22people_admin_job_level_id%22&user_id_type=open_id' \
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
	req := larkhire.NewGetByApplicationEmployeeReqBuilder().
		ApplicationId(`7379910335417927975`).
		UserIdType(`open_id`).
		DepartmentIdType(`"department_id"`).
		JobLevelIdType(`"people_admin_job_level_id"`).
		JobFamilyIdType(`"people_admin_job_category_id"`).
		EmployeeTypeIdType(`"people_admin_employee_type_id"`).
		Build()

	// 发起请求
	resp, err := client.Hire.V1.Employee.GetByApplication(context.Background(), req)

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
    request: GetByApplicationEmployeeRequest = GetByApplicationEmployeeRequest.builder() \
        .application_id("7379910335417927975") \
        .user_id_type("open_id") \
        .department_id_type(""department_id"") \
        .job_level_id_type(""people_admin_job_level_id"") \
        .job_family_id_type(""people_admin_job_category_id"") \
        .employee_type_id_type(""people_admin_employee_type_id"") \
        .build()

    # 发起请求
    response: GetByApplicationEmployeeResponse = client.hire.v1.employee.get_by_application(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.hire.v1.employee.get_by_application failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
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
public class GetByApplicationEmployeeSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      GetByApplicationEmployeeReq req = GetByApplicationEmployeeReq.newBuilder()
             .applicationId("7379910335417927975")
             .userIdType("open_id")
             .departmentIdType(""department_id"")
             .jobLevelIdType(""people_admin_job_level_id"")
             .jobFamilyIdType(""people_admin_job_category_id"")
             .employeeTypeIdType(""people_admin_employee_type_id"")
             .build();

      // 发起请求
      GetByApplicationEmployeeResp resp = client.hire().v1().employee().getByApplication(req);

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

client.hire.v1.employee.getByApplication({
        params: {
                application_id:'7379910335417927975',
                user_id_type:'open_id',
                department_id_type:'"department_id"',
                job_level_id_type:'"people_admin_job_level_id"',
                job_family_id_type:'"people_admin_job_category_id"',
                employee_type_id_type:'"people_admin_employee_type_id"',
        },
},
    lark.withTenantToken("t-7f1b******8e560")
).then(res => {
    console.log(res);
}).catch(e => {
    console.error(JSON.stringify(e.response.data, null, 4));
});

```

