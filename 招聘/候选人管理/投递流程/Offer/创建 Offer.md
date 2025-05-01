## 创建 Offer

传入 Offer 基本信息，创建 Offer。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/hire/v1/offers` |
| HTTP Method | POST |
| 支持的访问令牌 | tenant_access_token |
| 支持的应用类型 | custom |
| 权限要求 | 更新 offer 信息 <br> 获取用户 user ID |
| 权限要求 | hire:offer |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| user_id_type | string | 否 | 用户 ID 类型 |
| department_id_type | string | 否 | 此次调用中使用的部门 ID 类型。 |
| job_level_id_type | string | 否 | 此次调用中使用的「职级 ID」的类型 |
| job_family_id_type | string | 否 | 此次调用中使用的「序列 ID」的类型 |
| employee_type_id_type | string | 否 | 此次调用中使用的「人员类型 ID」的类型 |
### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| application_id | string | 是 | 投递 ID，详情请参考：[获取投递列表](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/application/list) <br> **示例**: 7013552389293279532  |
| schema_id | string | 否 | Offer 申请表模板 ID，用于描述申请表单结构的元数据定义，即对申请表内容的描述。用户每一次更改 Offer 申请表模板信息，都会生成新的 schema_id，创建 Offer 时应传入最新的 schema_id，可先从[获取职位设置](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/job/config)中拿到offer申请表ID，再从[获取 Offer 申请表信息](/ssl:ttdoc/ukTMukTMukTM/uMzM1YjLzMTN24yMzUjN/hire-v1/offer_application_form/get)接口中获取最新的模板ID。不填则会自动填充最新模版ID。 <br> **示例**: 7013318077945596204  |
| offer_type | integer | 否 | Offer 类型 <br> **示例**: 1 <br> **可选值**:<br>- 1: 正式 Offer <br>- 2: 实习 Offer <br> |
| basic_info | object | 是 | Offer 基本信息 <br> **示例**:   |
| salary_info | object | 否 | Offer 薪资信息 <br> **示例**:   |
| customized_info_list | offer_customized_info[] | 否 | 自定义信息 <br> **示例**:   |

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
    "application_id": "7013552389293279532",
    "schema_id": "7013318077945596204",
    "offer_type": 1,
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
        "job_requirement_id": "2342352224",
        "job_process_type_id": 2,
        "attachment_id_list": [
            "6792436415209817600"
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
    "msg": "success",
    "data": {
        "offer_id": "7016605170635213100",
        "application_id": "7013552389293279532",
        "schema_id": "7013318077945596204",
        "offer_type": 1,
        "basic_info": {
            "department_id": "od-6b394871807047c7023ebfc1ff37cd3a",
            "leader_user_id": "ou_ce613028fe74745421f5dc320bb9c709",
            "employment_job_id": "123",
            "employee_type_id": "2",
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
            "job_requirement_id": "2342352224",
            "job_process_type_id": 2,
            "attachment_id_list": [
                "679243641520981760"
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
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 500 | 1002001 | 系统错误 | 请根据实际报错信息定位或咨询[技术支持](https://applink.feishu.cn/TLJpeNdW) |
| 400 | 1002002 | 参数错误 | 检查参数是否正确，例如类型，大小 |
| 500 | 1002053 | offer already exist | Offer 已存在，不可重复创建 Offer |
| 500 | 1002054 | application not exist | 投递不存在，检查投递 ID 是否正确 |
| 500 | 1002055 | application already terminated | 投递已终止，不可发起 Offer |
| 500 | 1002056 | application stage abnormal | 投递阶段异常，检查投递状态 |
| 500 | 1002057 | schema not the latest version | 需传入最新版本的 schema_id |
| 500 | 1002058 | offer attachment not exist | 附件不存在，检查附件信息 |
| 500 | 1002059 | schema not exist | schema不存在，检查 schema_id |
| 500 | 1002061 | formula illegal | 检查公式信息 |
| 500 | 1002062 | miss in job process | 该投递阶段不支持创建 Offer |
| 400 | 1002069 | 职务不存在 | 请检查`employment_job_id `参数 |
| 400 | 1002070 | 职务已停用 | 请检查`employment_job_id `参数 |
| 400 | 1002071 | 序列不存在 | 请检查`job_family_id `参数 |
| 400 | 1002072 | 序列已停用 | 请检查`job_family_id `参数 |
| 400 | 1002073 | 职级不存在 | 请检查`job_level_id `参数 |
| 400 | 1002074 | 职级已停用 | 请检查`job_level_id `参数 |
| 400 | 1002075 | 职等不存在 | \- |
| 400 | 1002076 | 职等已停用 | \- |
| 400 | 1002077 | 职务、序列不匹配 | 请检查`employment_job_id `、`job_family_id `参数 |
| 400 | 1002078 | 职务、职级不匹配 | 请检查`employment_job_id `、`job_level_id `参数 |
| 400 | 1002079 | 序列、职级不匹配(在序列与职级在生效时间内未查询到关联的生效职务) | 请检查`job_family_id `、`job_level_id `参数 |
| 400 | 1002080 | 职级、职等不匹配 | \- |
| 400 | 1002082 | Offer 附件数量超过限制 | Offer 附件每个请求最多 20 个，请减少请求中的 Offer 附件数量 |
| 400 | 1002083 | Offer 附件对应的文件不存在 | 请检查附件 ID 是否合法 |

### 调用示例

#### Curl

```bash
curl -i -X POST 'https://open.feishu.cn/open-apis/hire/v1/offers?department_id_type=%22department_id%22&employee_type_id_type=%22people_admin_employee_type_id%22&job_family_id_type=%22people_admin_job_category_id%22&job_level_id_type=%22department_id%22&user_id_type=open_id' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"application_id": "7013552389293279532",
	"basic_info": {
		"attachment_description": "张三的简历",
		"attachment_id_list": [
			"6792436415209817600"
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
		"job_requirement_id": "2342352224",
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
	"offer_type": 1,
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
	req := larkhire.NewCreateOfferReqBuilder().
		UserIdType(`open_id`).
		DepartmentIdType(`"department_id"`).
		JobLevelIdType(`"department_id"`).
		JobFamilyIdType(`"people_admin_job_category_id"`).
		EmployeeTypeIdType(`"people_admin_employee_type_id"`).
		OfferInfo(larkhire.NewOfferInfoBuilder().
			ApplicationId(`7013552389293279532`).
			SchemaId(`7013318077945596204`).
			OfferType(1).
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
				JobRequirementId(`2342352224`).
				JobProcessTypeId(2).
				AttachmentIdList([]string{`6792436415209817600`}).
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
	resp, err := client.Hire.V1.Offer.Create(context.Background(), req)

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
    request: CreateOfferRequest = CreateOfferRequest.builder() \
        .user_id_type("open_id") \
        .department_id_type(""department_id"") \
        .job_level_id_type(""department_id"") \
        .job_family_id_type(""people_admin_job_category_id"") \
        .employee_type_id_type(""people_admin_employee_type_id"") \
        .request_body(OfferInfo.builder()
            .application_id("7013552389293279532")
            .schema_id("7013318077945596204")
            .offer_type(1)
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
                .job_requirement_id("2342352224")
                .job_process_type_id(2)
                .attachment_id_list(["6792436415209817600"])
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
    response: CreateOfferResponse = client.hire.v1.offer.create(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.hire.v1.offer.create failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
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
public class CreateOfferSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      CreateOfferReq req = CreateOfferReq.newBuilder()
             .userIdType("open_id")
             .departmentIdType(""department_id"")
             .jobLevelIdType(""department_id"")
             .jobFamilyIdType(""people_admin_job_category_id"")
             .employeeTypeIdType(""people_admin_employee_type_id"")
             .offerInfo(OfferInfo.newBuilder()
                 .applicationId("7013552389293279532")
                 .schemaId("7013318077945596204")
                 .offerType(1)
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
                        .jobRequirementId("2342352224")
                        .jobProcessTypeId(2)
                        .attachmentIdList(new String[]{"6792436415209817600"})
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
      CreateOfferResp resp = client.hire().v1().offer().create(req);

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

client.hire.v1.offer.create({
        params: {
                user_id_type:'open_id',
                department_id_type:'"department_id"',
                job_level_id_type:'"department_id"',
                job_family_id_type:'"people_admin_job_category_id"',
                employee_type_id_type:'"people_admin_employee_type_id"',
        },
        data: {
                application_id:'7013552389293279532',
                schema_id:'7013318077945596204',
                offer_type:1,
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
                        job_requirement_id:'2342352224',
                        job_process_type_id:2,
                        attachment_id_list:['6792436415209817600'],
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
var client = new RestClient("https://open.feishu.cn/open-apis/hire/v1/offers?department_id_type=%22department_id%22&employee_type_id_type=%22people_admin_employee_type_id%22&job_family_id_type=%22people_admin_job_category_id%22&job_level_id_type=%22department_id%22&user_id_type=open_id");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"application_id\":\"7013552389293279532\",\"basic_info\":{\"attachment_description\":\"张三的简历\",\"attachment_id_list\":[\"6792436415209817600\"],\"common_attachment_id_list\":[\"7483412052430997804\"],\"contract_period\":{\"period\":3,\"period_type\":1},\"contract_year\":3,\"department_id\":\"od-6b394871807047c7023ebfc1ff37cd3a\",\"employee_type_id\":\"6807407987381831949\",\"employment_job_id\":\"6807407987381831949\",\"expected_onboard_date\":\"{\\\"date\\\":\\\"2022-04-07\\\"}\",\"job_family_id\":\"6807407987381831949\",\"job_grade_id\":\"6897079709306259720\",\"job_level_id\":\"6807407987381881101\",\"job_offered\":\"入职职位\",\"job_process_type_id\":2,\"job_requirement_id\":\"2342352224\",\"leader_user_id\":\"ou_ce613028fe74745421f5dc320bb9c709\",\"onboard_address_id\":\"6897079709306259719\",\"operator_user_id\":\"ou_ce613028fe74745421f5dc320bb9c709\",\"owner_user_id\":\"ou_ce613028fe74745421f5dc320bb9c709\",\"position_id\":\"6897079709306259719\",\"probation_month\":3,\"recommended_words\":\"十分优秀，推荐入职\",\"work_address_id\":\"6897079709306259719\"},\"customized_info_list\":[{\"id\":\"6972464088568269100\",\"value\":\"1\"}],\"offer_type\":1,\"salary_info\":{\"award_salary_multiple\":\"3\",\"basic_salary\":\"1000000\",\"currency\":\"CNY\",\"half_year_bonus\":\"10000\",\"option_shares\":\"30\",\"probation_salary_percentage\":\"0.8\",\"quarterly_bonus\":\"3000\"},\"schema_id\":\"7013318077945596204\"}";
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
    "application_id": "7013552389293279532",
    "schema_id": "7013318077945596204",
    "offer_type": 1,
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
        "job_requirement_id": "2342352224",
        "job_process_type_id": 2,
        "attachment_id_list": [
            "6792436415209817600"
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
$request = new Request('POST', 'https://open.feishu.cn/open-apis/hire/v1/offers?department_id_type=%22department_id%22&employee_type_id_type=%22people_admin_employee_type_id%22&job_family_id_type=%22people_admin_job_category_id%22&job_level_id_type=%22department_id%22&user_id_type=open_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

