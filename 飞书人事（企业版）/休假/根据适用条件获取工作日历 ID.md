## 根据适用条件获取工作日历 ID

根据日历的适用范围，获取工作日历 ID。适用范围包含工作地点，工时制度等。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/corehr/v1/leaves/calendar_by_scope` |
| HTTP Method | GET |
| 支持的访问令牌 | tenant_access_token, user_access_token |
| 支持的应用类型 | custom  isv |
| 权限要求 | 获取核心人事信息 <br> 获取休假信息 <br> 查询工作日历 |
| 权限要求 | corehr:corehr:readonly <br> corehr:leave:read <br> corehr:work_calendar:read |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| wk_department_id | string | 否 | 用户所属部门的ID列表。
可以通过[批量查询任职信息](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/corehr-v1/job_data/list)获取所属部门的 ID |
| wk_country_region_id | string | 否 | 国家/地区 ID。
可以通过[批量查询任职信息](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/corehr-v1/job_data/list) 获取所属国家/地区 ID |
| wk_employee_type_id | string | 否 | 人员类型ID。
可以通过[批量查询任职信息](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/corehr-v1/job_data/list) 获取所属人员类型ID |
| wk_work_location_id | string | 否 | 工作地点ID。
可以通过[批量查询任职信息](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/corehr-v1/job_data/list) 获取工作地点ID |
| wk_working_hours_type_id | string | 否 | 工时制度ID。
可以通过[批量查询任职信息](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/corehr-v1/job_data/list) 获取工时制度ID |
| wk_job_family_id | string | 否 | 职务序列ID。
可以通过[批量查询任职信息](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/corehr-v1/job_data/list) 获取职务序列ID。 |
| wk_company_id | string | 否 | 公司 ID。
可以通过[批量查询任职信息](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/corehr-v1/job_data/list)获取公司 ID |
### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "calendar_wk_id": "6722331851580982798"
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 400 | 1160001 | param is invalid | 参数错误,<br>租户ID为空或者必填参数没有传入。 |
| 400 | 1160002 | GetEmploymentCalendar failed | 获取日历错误，请联系[技术支持](https://applink.feishu.cn/TLJpeNdW) 。 |
| 400 | 1160003 | GetByCalendarID failed | 根据日历获取详情错误，请联系[技术支持](https://applink.feishu.cn/TLJpeNdW) 。 |

### 调用示例

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
	req := larkcorehr.NewCalendarByScopeLeaveReqBuilder().
		WkDepartmentId(`"6722331851580982798"

`).
		WkCountryRegionId(`"6722331851580982798"

`).
		WkEmployeeTypeId(`"6722331851580982798"

`).
		WkWorkLocationId(`"6722331851580982798"
`).
		WkWorkingHoursTypeId(`"6722331851124982728"

`).
		WkJobFamilyId(`"8234534456354534546"
`).
		WkCompanyId(`"6235435355464465434"
`).
		Build()

	// 发起请求
	resp, err := client.Corehr.V1.Leave.CalendarByScope(context.Background(), req)

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
    request: CalendarByScopeLeaveRequest = CalendarByScopeLeaveRequest.builder() \
        .wk_department_id(""6722331851580982798"

") \
        .wk_country_region_id(""6722331851580982798"

") \
        .wk_employee_type_id(""6722331851580982798"

") \
        .wk_work_location_id(""6722331851580982798"
") \
        .wk_working_hours_type_id(""6722331851124982728"

") \
        .wk_job_family_id(""8234534456354534546"
") \
        .wk_company_id(""6235435355464465434"
") \
        .build()

    # 发起请求
    response: CalendarByScopeLeaveResponse = client.corehr.v1.leave.calendar_by_scope(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.corehr.v1.leave.calendar_by_scope failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
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
public class CalendarByScopeLeaveSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      CalendarByScopeLeaveReq req = CalendarByScopeLeaveReq.newBuilder()
             .wkDepartmentId(""6722331851580982798"

")
             .wkCountryRegionId(""6722331851580982798"

")
             .wkEmployeeTypeId(""6722331851580982798"

")
             .wkWorkLocationId(""6722331851580982798"
")
             .wkWorkingHoursTypeId(""6722331851124982728"

")
             .wkJobFamilyId(""8234534456354534546"
")
             .wkCompanyId(""6235435355464465434"
")
             .build();

      // 发起请求
      CalendarByScopeLeaveResp resp = client.corehr().v1().leave().calendarByScope(req);

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

client.corehr.v1.leave.calendarByScope({
        params: {
                wk_department_id:'"6722331851580982798"

',
                wk_country_region_id:'"6722331851580982798"

',
                wk_employee_type_id:'"6722331851580982798"

',
                wk_work_location_id:'"6722331851580982798"
',
                wk_working_hours_type_id:'"6722331851124982728"

',
                wk_job_family_id:'"8234534456354534546"
',
                wk_company_id:'"6235435355464465434"
',
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
var client = new RestClient("https://open.feishu.cn/open-apis/corehr/v1/leaves/calendar_by_scope?wk_company_id=%226235435355464465434%22%0A&wk_country_region_id=%226722331851580982798%22%0A%0A&wk_department_id=%226722331851580982798%22%0A%0A&wk_employee_type_id=%226722331851580982798%22%0A%0A&wk_job_family_id=%228234534456354534546%22%0A&wk_work_location_id=%226722331851580982798%22%0A&wk_working_hours_type_id=%226722331851124982728%22%0A%0A");
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
$request = new Request('GET', 'https://open.feishu.cn/open-apis/corehr/v1/leaves/calendar_by_scope?wk_company_id=%226235435355464465434%22%0A&wk_country_region_id=%226722331851580982798%22%0A%0A&wk_department_id=%226722331851580982798%22%0A%0A&wk_employee_type_id=%226722331851580982798%22%0A%0A&wk_job_family_id=%228234534456354534546%22%0A&wk_work_location_id=%226722331851580982798%22%0A&wk_working_hours_type_id=%226722331851124982728%22%0A%0A', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X GET 'https://open.feishu.cn/open-apis/corehr/v1/leaves/calendar_by_scope?wk_company_id=%226235435355464465434%22%0A&wk_country_region_id=%226722331851580982798%22%0A%0A&wk_department_id=%226722331851580982798%22%0A%0A&wk_employee_type_id=%226722331851580982798%22%0A%0A&wk_job_family_id=%228234534456354534546%22%0A&wk_work_location_id=%226722331851580982798%22%0A&wk_working_hours_type_id=%226722331851124982728%22%0A%0A' \
-H 'Authorization: Bearer t-7f1b******8e560'
```

