# 导入 e-HR（实习 Offer）

飞书招聘系统内用户选择实习 Offer 导入 e-HR 系统之后，将通过该事件推送候选人信息。{使用示例}(url=/api/tools/api_explore/api_explore_config?project=hire&version=v1&resource=ehr_import_task_for_internship_offer&event=imported)

<md-alert type="error">

</md-alert>


<md-alert type="warn">

</md-alert>


<md-alert type="tip">
- 需通过 更新 e-HR 导入任务结果 更新本次导入e-HR任务的结果


- 可以使用`offer_id ` 更新实习 Offer 入/离职状态
</md-alert>




## 事件
| 基本 |  |
| --- | --- |
| hire.ehr_import_task_for_internship_offer.imported_v1 |
|  |
| 更新导入 e-HR 任务 |
| <br> 该接口返回体中存在下列敏感字段，仅当开启对应的权限后才会返回；如果无需获取这些字段，则不建议申请<br> <br> 获取用户 user ID |
| `Webhook` |





### 事件体
<md-dt-table>
  <md-dt-thead>
      <md-dt-tr>
      <md-dt-th style="width: 35%;">名称</md-dt-th>
      <md-dt-th style="width: 13%;">类型</md-dt-th>
      <md-dt-th style="width: 52%;">描述</md-dt-th>
      </md-dt-tr>
  </md-dt-thead>
  <md-dt-tbody>
      
<md-dt-tr level="0">
	<md-dt-td>
	schema
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	事件模式
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="0">
	<md-dt-td>
	header
	</md-dt-td>
	<md-dt-td>
	event_header
	</md-dt-td>
	<md-dt-td>
	事件头
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	event_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	事件 ID
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	event_type
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	事件类型
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	create_time
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	事件创建时间戳（单位：毫秒）
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	token
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	事件 Token
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	app_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	应用 ID
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	tenant_key
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	租户 Key
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="0">
	<md-dt-td>
	event
	</md-dt-td>
	<md-dt-td>
	\-
	</md-dt-td>
	<md-dt-td>
	\-
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	task_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	导入任务 ID
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	application_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	投递 ID，详情请参考获取投递信息
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	offer_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	Offer ID，详情请参考获取 Offer 详情
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	pre_onboard_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	入职ID（实习）

	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	ehr_department_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	导入部门 ID，等同于`ehr_department. department_id`字段
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	operator_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	操作人的用户user id，等同于`operator_user_id.user_id`字段
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	operator_user_id
	</md-dt-td>
	<md-dt-td>
	user_id
	</md-dt-td>
	<md-dt-td>
	操作人用户 ID
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="2">
	<md-dt-td>
	union_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	用户的 union id
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="2">
	<md-dt-td>
	user_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	用户的 user id

**字段权限要求**：
获取用户 user ID
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="2">
	<md-dt-td>
	open_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	用户的 open id
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	ehr_department
	</md-dt-td>
	<md-dt-td>
	department_id
	</md-dt-td>
	<md-dt-td>
	导入部门ID
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="2">
	<md-dt-td>
	department_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	导入部门的部门 ID
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="2">
	<md-dt-td>
	open_department_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	导入部门的飞书部门 ID
	</md-dt-td>
</md-dt-tr>

  </md-dt-tbody>
</md-dt-table>




### 事件体示例
<md-code-json>
{
    "schema": "2.0",
    "header": {
        "event_id": "5e3702a84e847582be8db7fb73283c02",
        "event_type": "hire.ehr_import_task_for_internship_offer.imported_v1",
        "create_time": "1608725989000",
        "token": "rvaYgkND1GOiu5MM0E1rncYC6PLtF7JV",
        "app_id": "cli_9f5343c580712544",
        "tenant_key": "2ca1d211f64f6438"
    },
    "event": {
        "task_id": "6890840517010000141",
        "application_id": "6891113078776137998",
        "offer_id": "6930815272790114324",
        "pre_onboard_id": "6030815272790115431",
        "ehr_department_id": "6887399523094627847",
        "operator_id": "e33ggbyz",
        "operator_user_id": {
            "union_id": "on_8ed6aa67826108097d9ee143816345",
            "user_id": "e33ggbyz",
            "open_id": "ou_84aad35d084aa403a838cf73ee18467"
        },
        "ehr_department": {
            "department_id": "6887399523094627847",
            "open_department_id": "od-13d9a8f63abc60673fccaa2ed4dfcfb6"
        }
    }
}
</md-code-json>







### 事件订阅示例代码

事件订阅流程可参考：事件订阅概述，新手入门可参考：教程

<div style="margin-bottom: 4px;display: flex;column-gap: 4px;align-items: center;">
  订阅方式
  <md-tooltip>
    <ul class="md_render-table_solid md_render-table">
      <li><b>长连接方式（推荐）：</b>无需发布到公网地址，在本地开发环境中即可接收事件回调，且无需处理加解密逻辑。</li>
      <li><b>发送至开发者服务器：</b>需要提供服务器公网地址。</li>
    </ul>
  </md-tooltip>
</div>


<md-code-tabs>
  <md-code-tab-group title="使用长连接接收事件">
	
    <md-code-tab-panel sdkType="golang-sdk">
package main

import (
	"context"
	"fmt"

	larkcore "github.com/larksuite/oapi-sdk-go/v3/core"
	larkevent "github.com/larksuite/oapi-sdk-go/v3/event"
	"github.com/larksuite/oapi-sdk-go/v3/event/dispatcher"
	"github.com/larksuite/oapi-sdk-go/v3/service/hire/v1"
	larkws "github.com/larksuite/oapi-sdk-go/v3/ws"
)

// SDK 使用说明 SDK user guide：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
func main() {
	// 注册事件 Register event
	eventHandler := dispatcher.NewEventDispatcher("", "").
		OnP2EhrImportTaskForInternshipOfferImportedV1(func(ctx context.Context, event *larkhire.P2EhrImportTaskForInternshipOfferImportedV1) error {
			fmt.Printf("[ OnP2EhrImportTaskForInternshipOfferImportedV1 access ], data: %s\n", larkcore.Prettify(event))
			return nil
		})

	// 构建 client Build client
	cli := larkws.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET",
		larkws.WithEventHandler(eventHandler),
		larkws.WithLogLevel(larkcore.LogLevelDebug),
	)

	// 建立长连接 Establish persistent connection
	err := cli.Start(context.Background())

	if err != nil {
		panic(err)
	}
}

    </md-code-tab-panel>

    <md-code-tab-panel sdkType="python-sdk">
# SDK 使用说明 SDK user guide：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/python--sdk/preparations-before-development
import lark_oapi as lark


def do_p2_hire_ehr_import_task_for_internship_offer_imported_v1(data: lark.hire.v1.P2HireEhrImportTaskForInternshipOfferImportedV1) -> None:
    print(f'[ do_p2_hire_ehr_import_task_for_internship_offer_imported_v1 access ], data: {lark.JSON.marshal(data, indent=4)}')

# 注册事件 Register event
event_handler = lark.EventDispatcherHandler.builder("", "") \
    .register_p2_hire_ehr_import_task_for_internship_offer_imported_v1(do_p2_hire_ehr_import_task_for_internship_offer_imported_v1) \
    .build()


def main():
    # 构建 client Build client
    cli = lark.ws.Client("APP_ID", "APP_SECRET",
                        event_handler=event_handler, log_level=lark.LogLevel.DEBUG)
    # 建立长连接 Establish persistent connection
    cli.start()

if __name__ == "__main__":
    main()

    </md-code-tab-panel>

    <md-code-tab-panel sdkType="java-sdk">

package com.example.sample;

import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.hire.HireService;
import com.lark.oapi.service.hire.v1.model.P2EhrImportTaskForInternshipOfferImportedV1;
import com.lark.oapi.event.EventDispatcher;
import com.lark.oapi.ws.Client;

// SDK 使用说明 SDK user guide：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
public class Sample {
    // 注册事件 Register event
    private static final EventDispatcher EVENT_HANDLER = EventDispatcher.newBuilder("", "")
            .onP2EhrImportTaskForInternshipOfferImportedV1(new HireService.P2EhrImportTaskForInternshipOfferImportedV1Handler() {
                @Override
                public void handle(P2EhrImportTaskForInternshipOfferImportedV1 event) throws Exception {
                    System.out.printf("[ onP2EhrImportTaskForInternshipOfferImportedV1 access ], data: %s\n", Jsons.DEFAULT.toJson(event.getEvent()));
                }
            })
            .build();

    public static void main(String[] args) {
        // 构建 client Build client
        Client client = new Client.Builder("APP_ID", "APP_SECRET")
                .eventHandler(EVENT_HANDLER)
                .build();
        // 建立长连接 Establish persistent connection
        client.start();
    }
}
    </md-code-tab-panel>

    <md-code-tab-panel sdkType="nodejs-sdk">
// SDK 使用说明 SDK user guide：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/nodejs-sdk/preparation-before-development
import * as Lark from '@larksuiteoapi/node-sdk';
const baseConfig = {
    appId: 'APP_ID',
    appSecret: 'APP_SECRET'
}
// 构建 client Build client
const wsClient = new Lark.WSClient(baseConfig);
// 建立长连接 Establish persistent connection
wsClient.start({
    // 注册事件 Register event
    eventDispatcher: new Lark.EventDispatcher({}).register({
        'hire.ehr_import_task_for_internship_offer.imported_v1': async (data) => {
            console.log(data);
        }
    })
});
    </md-code-tab-panel>

  </md-code-tab-group>
  <md-code-tab-group title="将事件推送至开发者服务器">
	
    <md-code-tab-panel sdkType="golang-sdk">
package main

import (
	"context"
	"fmt"
	"net/http"

	larkcore "github.com/larksuite/oapi-sdk-go/v3/core"
	"github.com/larksuite/oapi-sdk-go/v3/core/httpserverext"
	larkevent "github.com/larksuite/oapi-sdk-go/v3/event"
	"github.com/larksuite/oapi-sdk-go/v3/event/dispatcher"
	"github.com/larksuite/oapi-sdk-go/v3/service/hire/v1"
)

// SDK 使用说明 SDK user guide：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
func main() {
	// 注册事件 Register event
	eventHandler := dispatcher.NewEventDispatcher("", "").
		OnP2EhrImportTaskForInternshipOfferImportedV1(func(ctx context.Context, event *larkhire.P2EhrImportTaskForInternshipOfferImportedV1) error {
			fmt.Printf("[ OnP2EhrImportTaskForInternshipOfferImportedV1 access ], data: %s\n", larkcore.Prettify(event))
			return nil
		})

	// 创建路由处理器 Create route handler
	http.HandleFunc("/webhook/event", httpserverext.NewEventHandlerFunc(handler, larkevent.WithLogLevel(larkcore.LogLevelDebug)))

	err := http.ListenAndServe(":7777", nil)

	if err != nil {
		panic(err)
	}
}

    </md-code-tab-panel>

    <md-code-tab-panel sdkType="python-sdk">
# SDK 使用说明 SDK user guide：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/python--sdk/preparations-before-development
from flask import Flask
from lark_oapi.adapter.flask import *
import lark_oapi as lark

app = Flask(__name__)


def do_p2_hire_ehr_import_task_for_internship_offer_imported_v1(data: lark.hire.v1.P2HireEhrImportTaskForInternshipOfferImportedV1) -> None:
    print(f'[ do_p2_hire_ehr_import_task_for_internship_offer_imported_v1 access ], data: {lark.JSON.marshal(data, indent=4)}')

# 注册事件 Register event
event_handler = lark.EventDispatcherHandler.builder("", "") \
    .register_p2_hire_ehr_import_task_for_internship_offer_imported_v1(do_p2_hire_ehr_import_task_for_internship_offer_imported_v1) \
    .build()


# 创建路由处理器 Create route handler
@app.route("/webhook/event", methods=["POST"])
def event():
    resp = handler.do(parse_req())
    return parse_resp(resp)

if __name__ == "__main__":
    app.run(port=7777)

    </md-code-tab-panel>

    <md-code-tab-panel sdkType="java-sdk">

package com.lark.oapi.sample.event;

import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.hire.HireService;
import com.lark.oapi.service.hire.v1.model.P2EhrImportTaskForInternshipOfferImportedV1;
import com.lark.oapi.sdk.servlet.ext.ServletAdapter;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

// SDK 使用说明 SDK user guide：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
@RestController
public class EventController {

    // 注册事件 Register event
    private static final EventDispatcher EVENT_HANDLER = EventDispatcher.newBuilder("verificationToken", "encryptKey")
            .onP2EhrImportTaskForInternshipOfferImportedV1(new HireService.P2EhrImportTaskForInternshipOfferImportedV1Handler() {
                @Override
                public void handle(P2EhrImportTaskForInternshipOfferImportedV1 event) throws Exception {
                    System.out.printf("[ onP2EhrImportTaskForInternshipOfferImportedV1 access ], data: %s\n", Jsons.DEFAULT.toJson(event.getEvent()));
                }
            })
            .build();

    // 注入 ServletAdapter 实例 Inject ServletAdapter instance
    @Autowired
    private ServletAdapter servletAdapter;

    // 创建路由处理器 Create route handler
    @RequestMapping("/webhook/event")
    public void event(HttpServletRequest request, HttpServletResponse response)
            throws Throwable {
        // 回调扩展包提供的事件回调处理器 Callback handler provided by the extension package
        servletAdapter.handleEvent(request, response, EVENT_DISPATCHER);
    }
}
    </md-code-tab-panel>

    <md-code-tab-panel sdkType="nodejs-sdk">
// SDK 使用说明 SDK user guide：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/nodejs-sdk/preparation-before-development
import http from 'http';
import * as lark from '@larksuiteoapi/node-sdk';

// 注册事件 Register event
const eventDispatcher = new lark.EventDispatcher({
    encryptKey: '',
    verificationToken: '',
}).register({
    'hire.ehr_import_task_for_internship_offer.imported_v1': async (data) => {
        console.log(data);
        return 'success';
    },
});

const server = http.createServer();
// 创建路由处理器 Create route handler
server.on('request', lark.adaptDefault('/webhook/event', eventDispatcher));
server.listen(3000);
    </md-code-tab-panel>

  </md-code-tab-group>
</md-code-tabs>

