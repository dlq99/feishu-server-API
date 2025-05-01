## 按 ID 查询考勤组

通过考勤组 ID 获取考勤组详情。包含基本信息、考勤班次、考勤方式、考勤设置信息

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/attendance/v1/groups/:group_id` |
| HTTP Method | GET |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom |
| 权限要求 | 写入打卡管理规则 <br> 导出打卡管理规则 |
| 权限要求 | attendance:rule <br> attendance:rule:readonly |

### 路径参数

| 参数名 | 类型 |  描述 |
| ------ | ---- | ---- |
| group_id | string | 考勤组 ID，获取方式：1）[创建或修改考勤组](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/attendance-v1/group/create) 2）[按名称查询考勤组](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/attendance-v1/group/search) 3）[获取打卡结果](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/attendance-v1/user_task/query) |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| employee_type | string | 是 | 请求体和响应体中的 user_id 和 creator_id 的员工id类型。如果没有后台管理权限，可使用[通过手机号或邮箱获取用户 ID](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/batch_get_id) |
| dept_type | string | 是 | 部门 ID 的类型 |
### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "group_id": "6919358128597097404",
        "group_name": "开心考勤",
        "time_zone": "Asia/Shanghai",
        "bind_dept_ids": [
            "od-fcb45c28a45311afd440b7869541fce8"
        ],
        "except_dept_ids": [
            "od-fcb45c28a45311afd440b7869541fce8"
        ],
        "bind_user_ids": [
            "52aa1fa1"
        ],
        "except_user_ids": [
            "4fasdtc2"
        ],
        "group_leader_ids": [
            "52aa1fa1"
        ],
        "sub_group_leader_ids": [
            "4fasdtc2"
        ],
        "allow_out_punch": true,
        "out_punch_need_approval": true,
        "out_punch_need_remark": true,
        "out_punch_need_photo": true,
        "out_punch_allowed_hide_addr": true,
        "allow_pc_punch": true,
        "allow_remedy": true,
        "remedy_limit": true,
        "remedy_limit_count": 3,
        "remedy_date_limit": true,
        "remedy_date_num": 3,
        "allow_remedy_type_lack": true,
        "allow_remedy_type_late": true,
        "allow_remedy_type_early": true,
        "allow_remedy_type_normal": true,
        "show_cumulative_time": true,
        "show_over_time": true,
        "hide_staff_punch_time": true,
        "face_punch": true,
        "face_punch_cfg": 1,
        "face_live_need_action": false,
        "face_downgrade": true,
        "replace_basic_pic": true,
        "machines": [
            {
                "machine_sn": "FS0701",
                "machine_name": "创实 9 楼"
            }
        ],
        "gps_range": 300,
        "locations": [
            {
                "location_id": "6921213751454744578",
                "location_name": "浙江省杭州市余杭区五常街道木桥头西溪八方城",
                "location_type": 1,
                "latitude": 30.28994,
                "longitude": 120.04509,
                "ssid": "TP-Link-af12ca",
                "bssid": "08:00:20:0A:8C:6D",
                "map_type": 1,
                "address": "北京市海淀区中航广场",
                "ip": "122.224.123.146",
                "feature": "中国电信",
                "gps_range": 300
            }
        ],
        "group_type": 0,
        "punch_day_shift_ids": [
            "xxx"
        ],
        "free_punch_cfg": {
            "free_start_time": "7:00",
            "free_end_time": "18:00",
            "punch_day": 1111100,
            "work_day_no_punch_as_lack": true,
            "work_hours_demand": false,
            "work_hours": 480
        },
        "calendar_id": 1,
        "need_punch_special_days": [
            {
                "punch_day": 20190101,
                "shift_id": "6919668827865513935"
            }
        ],
        "no_need_punch_special_days": [
            {
                "punch_day": 20190101,
                "shift_id": "6919668827865513935"
            }
        ],
        "work_day_no_punch_as_lack": true,
        "remedy_period_type": 1,
        "remedy_period_custom_date": 1,
        "punch_type": 1,
        "effect_time": "1611476284",
        "fixshift_effect_time": "1611476284",
        "member_effect_time": "1611476284",
        "rest_clockIn_need_approval": true,
        "clockIn_need_photo": true,
        "member_status_change": {
            "onboarding_on_no_need_punch": false,
            "onboarding_off_no_need_punch": false,
            "offboarding_on_no_need_punch": false,
            "offboarding_off_no_need_punch": false
        },
        "leave_need_punch": false,
        "leave_need_punch_cfg": {
            "late_minutes_as_late": 0,
            "late_minutes_as_lack": 0,
            "early_minutes_as_early": 0,
            "early_minutes_as_lack": 0
        },
        "go_out_need_punch": 0,
        "go_out_need_punch_cfg": {
            "late_minutes_as_late": 0,
            "late_minutes_as_lack": 0,
            "early_minutes_as_early": 0,
            "early_minutes_as_lack": 0
        },
        "travel_need_punch": 0,
        "travel_need_punch_cfg": {
            "late_minutes_as_late": 0,
            "late_minutes_as_lack": 0,
            "early_minutes_as_early": 0,
            "early_minutes_as_lack": 0
        },
        "need_punch_members": [
            {
                "rule_scope_type": 0,
                "scope_group_list": {
                    "scope_value_type": 1,
                    "operation_type": 1,
                    "right": [
                        {
                            "key": "CH",
                            "name": "中国大陆"
                        }
                    ],
                    "member_ids": [
                        "ec8ddg56"
                    ],
                    "custom_field_ID": "123213123",
                    "custom_field_obj_type": "employment"
                }
            }
        ],
        "no_need_punch_members": [
            {
                "rule_scope_type": 0,
                "scope_group_list": {
                    "scope_value_type": 1,
                    "operation_type": 1,
                    "right": [
                        {
                            "key": "CH",
                            "name": "中国大陆"
                        }
                    ],
                    "member_ids": [
                        "ec8ddg56"
                    ],
                    "custom_field_ID": "123213123",
                    "custom_field_obj_type": "employment"
                }
            }
        ],
        "save_auto_changes": false,
        "org_change_auto_adjust": false,
        "bind_default_dept_ids": [
            "od-fcb45c28a45311afd440b7869541fce8"
        ],
        "bind_default_user_ids": [
            "dd31248a"
        ]
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 400 | 1220001 | param is invalis | 入参校验失败，请根据具体返回的信息检查入参。例如“employee_type invalid”代表人员类型异常。如仍无法解决可联系 [技术支持](https://applink.feishu.cn/TLJpeNdW) |
| 400 | 1220002 | tenant_id is empty | 请检查入参中的 tenant_access_token是否正确 |
| 400 | 1220003 | user_id type is not employee_id or employee_no | employee_type只支持取值为 employee_id或者employee_no |
| 500 | 1225000 | param is invalis | 请参考实际返回的错误信息排查问题。例如“internal server error”代表内部服务异常。如仍无法解决可联系 [技术支持](https://applink.feishu.cn/TLJpeNdW) |
| 500 | 1227000 | 历史错误码，不再使用 | - |
| 400 | 1220600 | 通用错误信息 | 通用错误信息包含多条，详细的错误信息以及处理建议可参见 [错误信息](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/attendance-v1/attendance-development-guidelines) |

### 调用示例

#### Curl

```bash
curl -i -X GET 'https://open.feishu.cn/open-apis/attendance/v1/groups/6919358128597097404?dept_type=open_id&employee_type=employee_id' \
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
	"github.com/larksuite/oapi-sdk-go/v3/service/attendance/v1"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkattendance.NewGetGroupReqBuilder().
		GroupId(`6919358128597097404`).
		EmployeeType(`employee_id`).
		DeptType(`open_id`).
		Build()

	// 发起请求
	resp, err := client.Attendance.V1.Group.Get(context.Background(), req)

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
from lark_oapi.api.attendance.v1 import *


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
    request: GetGroupRequest = GetGroupRequest.builder() \
        .group_id("6919358128597097404") \
        .employee_type("employee_id") \
        .dept_type("open_id") \
        .build()

    # 发起请求
    response: GetGroupResponse = client.attendance.v1.group.get(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.attendance.v1.group.get failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

#### Java SDK

```java
package com.lark.oapi.sample.apiall.attendancev1;
import com.google.gson.JsonParser;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.attendance.v1.model.*;
import java.util.HashMap;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class GetGroupSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      GetGroupReq req = GetGroupReq.newBuilder()
             .groupId("6919358128597097404")
             .employeeType("employee_id")
             .deptType("open_id")
             .build();

      // 发起请求
      GetGroupResp resp = client.attendance().v1().group().get(req);

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

client.attendance.v1.group.get({
        path: {
                group_id:'6919358128597097404',
        },
        params: {
                employee_type:'employee_id',
                dept_type:'open_id',
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
var client = new RestClient("https://open.feishu.cn/open-apis/attendance/v1/groups/6919358128597097404?dept_type=open_id&employee_type=employee_id");
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
$request = new Request('GET', 'https://open.feishu.cn/open-apis/attendance/v1/groups/6919358128597097404?dept_type=open_id&employee_type=employee_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

