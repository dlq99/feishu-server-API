## 更新 Offer 信息

更新 Offer 信息，包含基本信息、薪资信息、自定义信息。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/hire/v1/offers/:offer_id` |
| HTTP Method | PUT |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom |
| 权限要求 | 更新 offer 信息 <br> 获取用户 user ID |
| 权限要求 | hire:offer |

### 路径参数

| 参数名 | 类型 |  描述 |
| ------ | ---- | ---- |
| offer_id | string | Offer ID，可通过[获取 Offer 列表](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/offer/list)接口获取 |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| user_id_type | string | 否 | 用户 ID 类型 |
| department_id_type | string | 否 | 指定查询结果中的部门 ID 类型。关于部门 ID 的详细介绍，可参见[部门资源介绍](/ssl:ttdoc/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview)。
 |
| job_level_id_type | string | 否 | 此次调用中使用的「职级 ID」的类型 |
| job_family_id_type | string | 否 | 此次调用中使用的「序列 ID」的类型 |
| employee_type_id_type | string | 否 | 此次调用中使用的「人员类型 ID」的类型 |
### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| schema_id | string | 是 | Offer 申请表模板 ID，用于描述申请表单结构的元数据定义，即对申请表内容的描述。用户每一次更改 Offer 申请表模板信息，都会生成新的 schema_id，创建 Offer 时应传入最新的 schema_id，可先从[获取职位设置](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/job/config)中拿到offer申请表 ID，再从[获取 Offer 申请表信息](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/offer_application_form/get)接口中获取最新的模板 ID。 <br> **示例**: 7013318077945596204  |
| basic_info | object | 是 | Offer 基本信息 <br> **示例**:   |
| salary_info | object | 否 | Offer 薪资信息 <br> **示例**:   |
| customized_info_list | offer_customized_info[] | 否 | 自定义信息，此字段更新为覆盖式更新，旧 Offer 中已存在字段不传则默认为删除，反之为新增 <br> **示例**:   |

**类型额外说明**:

- **offer_basic_info** 类型说明:

  基本属性:

   department_id: string <br> leader_user_id: string <br> employment_job_id: string <br> employee_type_id: string <br> job_family_id: string <br> job_level_id: string <br> probation_month: integer <br> contract_year: integer <br> expected_onboard_date: string <br> onboard_address_id: string <br> work_address_id: string <br> owner_user_id: string <br> recommended_words: string <br> job_requirement_id: string <br> job_process_type_id: integer <br> attachment_id_list: array <br> common_attachment_id_list: array <br> attachment_description: string <br> operator_user_id: string <br> position_id: string <br> job_offered: string <br> job_grade_id: string <br>
  - **contract_period** (object):
    - **contract_period_info** 类型说明:

      基本属性:

       period_type: integer <br> period: integer <br>
- **offer_salary_info** 类型说明:

  基本属性:

   currency: string <br> basic_salary: string <br> probation_salary_percentage: string <br> award_salary_multiple: string <br> option_shares: string <br> quarterly_bonus: string <br> half_year_bonus: string <br>
- **offer_customized_info** 类型说明:

  基本属性:

   id: string <br> value: string <br>


**请求体示例**:

```json
{
    "schema_id": "7013318077945596204",
    "basic_info": {
        "department_id": "od-6b394871807047c7023ebfc1ff37cd3a",
        "leader_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
        "employment_job_id": "6807407987381831949",
        "employee_type_id": "6807407987381831949",
        "job_family_id": "6807407987381831949",
        "job_level_id": "6807407987381881101",
        "probation_month": 3,
        "contract_year": 3,
        "contract_period": {
            "period_type": 1,
            "period": 3
        },
        "expected_onboard_date": "{\"date\":\"2022-04-07\"}",
        "onboard_address_id": "6897079709306259719",
        "work_address_id": "6897079709306259719",
        "owner_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
        "recommended_words": "十分优秀，推荐入职",
        "job_requirement_id": "6791698585114724616",
        "job_process_type_id": 2,
        "attachment_id_list": [
            "7159169181052061965"
        ],
        "common_attachment_id_list": [
            "7483412052430997804"
        ],
        "attachment_description": "张三的简历",
        "operator_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
        "position_id": "6897079709306259719",
        "job_offered": "入职职位",
        "job_grade_id": "6897079709306259720"
    },
    "salary_info": {
        "currency": "CNY",
        "basic_salary": "1000000",
        "probation_salary_percentage": "0.8",
        "award_salary_multiple": "3",
        "option_shares": "30",
        "quarterly_bonus": "3000",
        "half_year_bonus": "10000"
    },
    "customized_info_list": [
        {
            "id": "6972464088568269100",
            "value": "1"
        }
    ]
}
```

### 响应

**响应示例**:

```json
{
    "code": 0,
    "msg": "ok",
    "data": {
        "offer_id": "7016605170635213100",
        "schema_id": "7013318077945596204",
        "basic_info": {
            "department_id": "od-6b394871807047c7023ebfc1ff37cd3a",
            "leader_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
            "employment_job_id": "6807407987381831949",
            "employee_type_id": "6807407987381831949",
            "job_family_id": "6807407987381831949",
            "job_level_id": "6807407987381881101",
            "probation_month": 3,
            "contract_year": 3,
            "contract_period": {
                "period_type": 1,
                "period": 3
            },
            "expected_onboard_date": "{\"date\":\"2022-04-07\"}",
            "onboard_address_id": "6897079709306259719",
            "work_address_id": "6897079709306259719",
            "owner_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
            "recommended_words": "十分优秀，推荐入职",
            "job_requirement_id": "6791698585114724616",
            "job_process_type_id": 2,
            "attachment_id_list": [
                "7159169181052061965"
            ],
            "common_attachment_id_list": [
                "7483412052430997804"
            ],
            "attachment_description": "张三的简历",
            "operator_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
            "position_id": "6897079709306259719",
            "job_offered": "入职职位",
            "job_grade_id": "6897079709306259720"
        },
        "salary_info": {
            "currency": "CNY",
            "basic_salary": "1000000",
            "probation_salary_percentage": "0.8",
            "award_salary_multiple": "3",
            "option_shares": "11",
            "quarterly_bonus": "3000",
            "half_year_bonus": "10000"
        },
        "customized_info_list": [
            {
                "id": "6972464088568269100",
                "value": "1"
            }
        ]
    }
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 500 | 1002001 | 系统错误 | 请根据实际报错信息定位或咨询[技术支持](https://applink.feishu.cn/TLJpeNdW) |
| 400 | 1002002 | 参数错误 | 检查参数是否正确，例如类型，大小 |
| 500 | 1002054 | 投递不存在 | 投递不存在，根据参数`offer_id `未找到对应投递，请检查参数或使用[获取 Offer 详情](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/offer/get)接口查询对应 Offer 是否存在，以及确认接口返回值`application_id `<br> |
| 500 | 1002055 | 投递已经终止 | Offer 对应投递已终止，不可被更新，详情可根据[获取 Offer 详情](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/offer/get)接口查看投递 ID，再根据[获取投递信息](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/application/get)接口查看投递状态 |
| 500 | 1002056 | 投递阶段异常 | 投递阶段异常，详情可根据[获取 Offer 详情](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/offer/get)接口查看投递 ID，再根据[获取投递信息](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/application/get)接口查看投递阶段是否异常 |
| 500 | 1002057 | Offer 申请表模板不是最新的版本 | Offer 申请表模板不是最新的版本，请检查`schema_id `参数是否正确 |
| 500 | 1002058 | Offer 附件不存在 | Offer 附件不存在，请检查 `attachment_id_list `参数是否正确 |
| 500 | 1002059 | Offer 申请表模板不存在 | Offer 申请表模板不存在，请检查`schema_id `参数是否正确 |
| 500 | 1002061 | 公式无效 | 公式无效，请检查`customized_info_list `参数中公式相关 |
| 500 | 1002064 | Offer 不存在 | Offer 不存在，请检查`offer_id `参数是否正确 |
| 500 | 1002066 | Offer 状态不支持更新 | Offer 当前状态不支持更新，可根据[获取 Offer 详情](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/offer/get)接口查看 Offer 状态 |
| 400 | 1002069 | 职务不存在 | 职务不存在，请检查`employment_job_id `参数是否正确 |
| 400 | 1002070 | 职务已停用 | 职务已停用，请检查`employment_job_id `参数是否正确 |
| 400 | 1002071 | 序列不存在 | 序列不存在，请检查`job_family_id `参数是否正确 |
| 400 | 1002072 | 序列已停用 | 序列已停用，请检查`job_family_id `参数是否正确 |
| 400 | 1002073 | 职级不存在 | 职级不存在，请检查`job_level_id `参数是否正确 |
| 400 | 1002074 | 职级已停用 | 职级已停用，请检查`job_level_id `参数是否正确 |
| 400 | 1002077 | 职务、序列不匹配 | 职务、序列不匹配，请检查`employment_job_id `、`job_family_id `参数是否正确 |
| 400 | 1002078 | 职务、职级不匹配 | 职务、职级不匹配，请检查`employment_job_id `、`job_level_id `参数是否正确 |
| 400 | 1002079 | 序列、职级不匹配(在序列与职级在生效时间内未查询到关联的生效职务) | 序列、职级不匹配，请检查`job_family_id `、`job_level_id `参数是否正确 |
| 400 | 1002082 | Offer 附件数量超过限制 | Offer 附件每个请求最多 20 个，请减少请求中的 Offer 附件数量 |
| 400 | 1002083 | Offer 附件对应的文件不存在 | 请检查附件 ID 是否合法 |

### 调用示例

#### Curl

```bash
curl -i -X PUT 'https://open.feishu.cn/open-apis/hire/v1/offers/7016605170635213100?department_id_type=department_id&employee_type_id_type=employee_type_enum_id&job_family_id_type=job_family_id&job_level_id_type=job_level_id&user_id_type=open_id' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"basic_info": {
		"attachment_description": "张三的简历",
		"attachment_id_list": [
			"7159169181052061965"
		],
		"common_attachment_id_list": [
			"7483412052430997804"
		],
		"contract_period": {
			"period": 3,
			"period_type": 1
		},
		"contract_year": 3,
		"department_id": "od-6b394871807047c7023ebfc1ff37cd3a",
		"employee_type_id": "6807407987381831949",
		"employment_job_id": "6807407987381831949",
		"expected_onboard_date": "{\"date\":\"2022-04-07\"}",
		"job_family_id": "6807407987381831949",
		"job_grade_id": "6897079709306259720",
		"job_level_id": "6807407987381881101",
		"job_offered": "入职职位",
		"job_process_type_id": 2,
		"job_requirement_id": "6791698585114724616",
		"leader_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
		"onboard_address_id": "6897079709306259719",
		"operator_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
		"owner_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
		"position_id": "6897079709306259719",
		"probation_month": 3,
		"recommended_words": "十分优秀，推荐入职",
		"work_address_id": "6897079709306259719"
	},
	"customized_info_list": [
		{
			"id": "6972464088568269100",
			"value": "1"
		}
	],
	"salary_info": {
		"award_salary_multiple": "3",
		"basic_salary": "1000000",
		"currency": "CNY",
		"half_year_bonus": "10000",
		"option_shares": "30",
		"probation_salary_percentage": "0.8",
		"quarterly_bonus": "3000"
	},
	"schema_id": "7013318077945596204"
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
	req := larkhire.NewUpdateOfferReqBuilder().
		OfferId(`7016605170635213100`).
		UserIdType(`open_id`).
		DepartmentIdType(`department_id`).
		JobLevelIdType(`job_level_id`).
		JobFamilyIdType(`job_family_id`).
		EmployeeTypeIdType(`employee_type_enum_id`).
		OfferInfo(larkhire.NewOfferInfoBuilder().
			SchemaId(`7013318077945596204`).
			BasicInfo(larkhire.NewOfferBasicInfoBuilder().
				DepartmentId(`od-6b394871807047c7023ebfc1ff37cd3a`).
				LeaderUserId(`ou_ce613028fe74745421f5dc320bb9c709`).
				EmploymentJobId(`6807407987381831949`).
				EmployeeTypeId(`6807407987381831949`).
				JobFamilyId(`6807407987381831949`).
				JobLevelId(`6807407987381881101`).
				ProbationMonth(3).
				ContractYear(3).
				ContractPeriod(larkhire.NewContractPeriodInfoBuilder().
					PeriodType(1).
					Period(3).
					Build()).
				ExpectedOnboardDate(`{"date":"2022-04-07"}`).
				OnboardAddressId(`6897079709306259719`).
				WorkAddressId(`6897079709306259719`).
				OwnerUserId(`ou_ce613028fe74745421f5dc320bb9c709`).
				RecommendedWords(`十分优秀，推荐入职`).
				JobRequirementId(`6791698585114724616`).
				JobProcessTypeId(2).
				AttachmentIdList([]string{`7159169181052061965`}).
				CommonAttachmentIdList([]string{`7483412052430997804`}).
				AttachmentDescription(`张三的简历`).
				OperatorUserId(`ou_ce613028fe74745421f5dc320bb9c709`).
				PositionId(`6897079709306259719`).
				JobOffered(`入职职位`).
				JobGradeId(`6897079709306259720`).
				Build()).
			SalaryInfo(larkhire.NewOfferSalaryInfoBuilder().
				Currency(`CNY`).
				BasicSalary(`1000000`).
				ProbationSalaryPercentage(`0.8`).
				AwardSalaryMultiple(`3`).
				OptionShares(`30`).
				QuarterlyBonus(`3000`).
				HalfYearBonus(`10000`).
				Build()).
			CustomizedInfoList([]*larkhire.OfferCustomizedInfo{
				larkhire.NewOfferCustomizedInfoBuilder().
					Id(`6972464088568269100`).
					Value(`1`).
					Build(),
			}).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Hire.V1.Offer.Update(context.Background(), req)

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
    request: UpdateOfferRequest = UpdateOfferRequest.builder() \
        .offer_id("7016605170635213100") \
        .user_id_type("open_id") \
        .department_id_type("department_id") \
        .job_level_id_type("job_level_id") \
        .job_family_id_type("job_family_id") \
        .employee_type_id_type("employee_type_enum_id") \
        .request_body(OfferInfo.builder()
            .schema_id("7013318077945596204")
            .basic_info(OfferBasicInfo.builder()
                .department_id("od-6b394871807047c7023ebfc1ff37cd3a")
                .leader_user_id("ou_ce613028fe74745421f5dc320bb9c709")
                .employment_job_id("6807407987381831949")
                .employee_type_id("6807407987381831949")
                .job_family_id("6807407987381831949")
                .job_level_id("6807407987381881101")
                .probation_month(3)
                .contract_year(3)
                .contract_period(ContractPeriodInfo.builder()
                    .period_type(1)
                    .period(3)
                    .build())
                .expected_onboard_date("{\"date\":\"2022-04-07\"}")
                .onboard_address_id("6897079709306259719")
                .work_address_id("6897079709306259719")
                .owner_user_id("ou_ce613028fe74745421f5dc320bb9c709")
                .recommended_words("十分优秀，推荐入职")
                .job_requirement_id("6791698585114724616")
                .job_process_type_id(2)
                .attachment_id_list(["7159169181052061965"])
                .common_attachment_id_list(["7483412052430997804"])
                .attachment_description("张三的简历")
                .operator_user_id("ou_ce613028fe74745421f5dc320bb9c709")
                .position_id("6897079709306259719")
                .job_offered("入职职位")
                .job_grade_id("6897079709306259720")
                .build())
            .salary_info(OfferSalaryInfo.builder()
                .currency("CNY")
                .basic_salary("1000000")
                .probation_salary_percentage("0.8")
                .award_salary_multiple("3")
                .option_shares("30")
                .quarterly_bonus("3000")
                .half_year_bonus("10000")
                .build())
            .customized_info_list([OfferCustomizedInfo.builder()
                .id("6972464088568269100")
                .value("1")
                .build()
                ])
            .build()) \
        .build()

    # 发起请求
    response: UpdateOfferResponse = client.hire.v1.offer.update(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.hire.v1.offer.update failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
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
public class UpdateOfferSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      UpdateOfferReq req = UpdateOfferReq.newBuilder()
             .offerId("7016605170635213100")
             .userIdType("open_id")
             .departmentIdType("department_id")
             .jobLevelIdType("job_level_id")
             .jobFamilyIdType("job_family_id")
             .employeeTypeIdType("employee_type_enum_id")
             .offerInfo(OfferInfo.newBuilder()
                 .schemaId("7013318077945596204")
                 .basicInfo(OfferBasicInfo.newBuilder()
                        .departmentId("od-6b394871807047c7023ebfc1ff37cd3a")
                        .leaderUserId("ou_ce613028fe74745421f5dc320bb9c709")
                        .employmentJobId("6807407987381831949")
                        .employeeTypeId("6807407987381831949")
                        .jobFamilyId("6807407987381831949")
                        .jobLevelId("6807407987381881101")
                        .probationMonth(3)
                        .contractYear(3)
                        .contractPeriod(ContractPeriodInfo.newBuilder()
                          .periodType(1)
                          .period(3)
                          .build())
                        .expectedOnboardDate("{\"date\":\"2022-04-07\"}")
                        .onboardAddressId("6897079709306259719")
                        .workAddressId("6897079709306259719")
                        .ownerUserId("ou_ce613028fe74745421f5dc320bb9c709")
                        .recommendedWords("十分优秀，推荐入职")
                        .jobRequirementId("6791698585114724616")
                        .jobProcessTypeId(2)
                        .attachmentIdList(new String[]{"7159169181052061965"})
                        .commonAttachmentIdList(new String[]{"7483412052430997804"})
                        .attachmentDescription("张三的简历")
                        .operatorUserId("ou_ce613028fe74745421f5dc320bb9c709")
                        .positionId("6897079709306259719")
                        .jobOffered("入职职位")
                        .jobGradeId("6897079709306259720")
                        .build())
                 .salaryInfo(OfferSalaryInfo.newBuilder()
                        .currency("CNY")
                        .basicSalary("1000000")
                        .probationSalaryPercentage("0.8")
                        .awardSalaryMultiple("3")
                        .optionShares("30")
                        .quarterlyBonus("3000")
                        .halfYearBonus("10000")
                        .build())
                 .customizedInfoList(new OfferCustomizedInfo[]{
                    OfferCustomizedInfo.newBuilder()
                      .id("6972464088568269100")
                      .value("1")
                      .build()
                    })
                  .build())
             .build();

      // 发起请求
      UpdateOfferResp resp = client.hire().v1().offer().update(req);

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

client.hire.v1.offer.update({
        path: {
                offer_id:'7016605170635213100',
        },
        params: {
                user_id_type:'open_id',
                department_id_type:'department_id',
                job_level_id_type:'job_level_id',
                job_family_id_type:'job_family_id',
                employee_type_id_type:'employee_type_enum_id',
        },
        data: {
                schema_id:'7013318077945596204',
                basic_info:{
                        department_id:'od-6b394871807047c7023ebfc1ff37cd3a',
                        leader_user_id:'ou_ce613028fe74745421f5dc320bb9c709',
                        employment_job_id:'6807407987381831949',
                        employee_type_id:'6807407987381831949',
                        job_family_id:'6807407987381831949',
                        job_level_id:'6807407987381881101',
                        probation_month:3,
                        contract_year:3,
                        contract_period:{
                          period_type:1,
                          period:3,
                          },
                        expected_onboard_date:'{"date":"2022-04-07"}',
                        onboard_address_id:'6897079709306259719',
                        work_address_id:'6897079709306259719',
                        owner_user_id:'ou_ce613028fe74745421f5dc320bb9c709',
                        recommended_words:'十分优秀，推荐入职',
                        job_requirement_id:'6791698585114724616',
                        job_process_type_id:2,
                        attachment_id_list:['7159169181052061965'],
                        common_attachment_id_list:['7483412052430997804'],
                        attachment_description:'张三的简历',
                        operator_user_id:'ou_ce613028fe74745421f5dc320bb9c709',
                        position_id:'6897079709306259719',
                        job_offered:'入职职位',
                        job_grade_id:'6897079709306259720',
                        },
                salary_info:{
                        currency:'CNY',
                        basic_salary:'1000000',
                        probation_salary_percentage:'0.8',
                        award_salary_multiple:'3',
                        option_shares:'30',
                        quarterly_bonus:'3000',
                        half_year_bonus:'10000',
                        },
                customized_info_list:[
                    {
                      id:'6972464088568269100',
                      value:'1',
                      }
                    ],
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
var client = new RestClient("https://open.feishu.cn/open-apis/hire/v1/offers/7016605170635213100?department_id_type=department_id&employee_type_id_type=employee_type_enum_id&job_family_id_type=job_family_id&job_level_id_type=job_level_id&user_id_type=open_id");
client.Timeout = -1;
var request = new RestRequest(Method.PUT);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"basic_info\":{\"attachment_description\":\"张三的简历\",\"attachment_id_list\":[\"7159169181052061965\"],\"common_attachment_id_list\":[\"7483412052430997804\"],\"contract_period\":{\"period\":3,\"period_type\":1},\"contract_year\":3,\"department_id\":\"od-6b394871807047c7023ebfc1ff37cd3a\",\"employee_type_id\":\"6807407987381831949\",\"employment_job_id\":\"6807407987381831949\",\"expected_onboard_date\":\"{\\\"date\\\":\\\"2022-04-07\\\"}\",\"job_family_id\":\"6807407987381831949\",\"job_grade_id\":\"6897079709306259720\",\"job_level_id\":\"6807407987381881101\",\"job_offered\":\"入职职位\",\"job_process_type_id\":2,\"job_requirement_id\":\"6791698585114724616\",\"leader_user_id\":\"ou_ce613028fe74745421f5dc320bb9c709\",\"onboard_address_id\":\"6897079709306259719\",\"operator_user_id\":\"ou_ce613028fe74745421f5dc320bb9c709\",\"owner_user_id\":\"ou_ce613028fe74745421f5dc320bb9c709\",\"position_id\":\"6897079709306259719\",\"probation_month\":3,\"recommended_words\":\"十分优秀，推荐入职\",\"work_address_id\":\"6897079709306259719\"},\"customized_info_list\":[{\"id\":\"6972464088568269100\",\"value\":\"1\"}],\"salary_info\":{\"award_salary_multiple\":\"3\",\"basic_salary\":\"1000000\",\"currency\":\"CNY\",\"half_year_bonus\":\"10000\",\"option_shares\":\"30\",\"probation_salary_percentage\":\"0.8\",\"quarterly_bonus\":\"3000\"},\"schema_id\":\"7013318077945596204\"}";
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
    "schema_id": "7013318077945596204",
    "basic_info": {
        "department_id": "od-6b394871807047c7023ebfc1ff37cd3a",
        "leader_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
        "employment_job_id": "6807407987381831949",
        "employee_type_id": "6807407987381831949",
        "job_family_id": "6807407987381831949",
        "job_level_id": "6807407987381881101",
        "probation_month": 3,
        "contract_year": 3,
        "contract_period": {
            "period_type": 1,
            "period": 3
        },
        "expected_onboard_date": "{\"date\":\"2022-04-07\"}",
        "onboard_address_id": "6897079709306259719",
        "work_address_id": "6897079709306259719",
        "owner_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
        "recommended_words": "十分优秀，推荐入职",
        "job_requirement_id": "6791698585114724616",
        "job_process_type_id": 2,
        "attachment_id_list": [
            "7159169181052061965"
        ],
        "common_attachment_id_list": [
            "7483412052430997804"
        ],
        "attachment_description": "张三的简历",
        "operator_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
        "position_id": "6897079709306259719",
        "job_offered": "入职职位",
        "job_grade_id": "6897079709306259720"
    },
    "salary_info": {
        "currency": "CNY",
        "basic_salary": "1000000",
        "probation_salary_percentage": "0.8",
        "award_salary_multiple": "3",
        "option_shares": "30",
        "quarterly_bonus": "3000",
        "half_year_bonus": "10000"
    },
    "customized_info_list": [
        {
            "id": "6972464088568269100",
            "value": "1"
        }
    ]
}';
$request = new Request('PUT', 'https://open.feishu.cn/open-apis/hire/v1/offers/7016605170635213100?department_id_type=department_id&employee_type_id_type=employee_type_enum_id&job_family_id_type=job_family_id&job_level_id_type=job_level_id&user_id_type=open_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

