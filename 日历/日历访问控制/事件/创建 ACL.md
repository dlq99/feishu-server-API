# 创建 ACL

当订阅的日历上有访问控制被创建时，将会触发此事件。{使用示例}(url=/api/tools/api_explore/api_explore_config?project=calendar&version=v4&resource=calendar.acl&event=created)

<md-alert type="error">

</md-alert>


<md-alert type="warn">
你需要先为用户订阅日历访问控制变更事件，并且需要在应用中配置事件订阅，这样才可以在事件触发时接收到事件数据。了解事件订阅参见事件订阅概述。
</md-alert>


<md-alert type="tip">

</md-alert>




## 事件
| 基本 |  |
| --- | --- |
| calendar.calendar.acl.created_v4 |
|  |
| 更新日历及日程信息<br> 读取日历访问控制权限<br> 获取日历、日程及忙闲信息 |
| <br> 该接口返回体中存在下列敏感字段，仅当开启对应的权限后才会返回；如果无需获取这些字段，则不建议申请<br> <br> 获取用户 user ID |
| `Webhook` |





### 事件体
<md-dt-table>
  <md-dt-thead>
      <md-dt-tr>
      <md-dt-th style="width: 40%;">名称</md-dt-th>
      <md-dt-th style="width: 20%;">类型</md-dt-th>
      <md-dt-th style="width: 30%;">描述</md-dt-th>
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
	calendar.acl_event
	</md-dt-td>
	<md-dt-td>
	\-
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	acl_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	访问控制 ID。该 ID 在单个日历实体内唯一，不同日历实体可能存在重复的访问控制 ID。
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	role
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	对日历的访问权限。

**可选值有**：
<md-enum>
<md-enum-item key="unknown" >未知权限。</md-enum-item>
<md-enum-item key="free_busy_reader" >游客，只能看到忙碌、空闲信息。</md-enum-item>
<md-enum-item key="reader" >订阅者，可查看所有日程详情。</md-enum-item>
<md-enum-item key="writer" >编辑者，可创建及修改日程。</md-enum-item>
<md-enum-item key="owner" >管理员，可管理日历及共享设置。</md-enum-item>
</md-enum>
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="1">
	<md-dt-td>
	scope
	</md-dt-td>
	<md-dt-td>
	acl_scope_event
	</md-dt-td>
	<md-dt-td>
	权限生效范围。
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="2">
	<md-dt-td>
	type
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	权限生效范围的类型。

**可选值有**：
<md-enum>
<md-enum-item key="user" >用户</md-enum-item>
</md-enum>
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="2">
	<md-dt-td>
	user_id
	</md-dt-td>
	<md-dt-td>
	user_id
	</md-dt-td>
	<md-dt-td>
	用户 ID
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="3">
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


<md-dt-tr level="3">
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


<md-dt-tr level="3">
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
	user_id_list
	</md-dt-td>
	<md-dt-td>
	user_id\[\]
	</md-dt-td>
	<md-dt-td>
	需要推送事件的用户列表。
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
	用户的 union_id。
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
	用户的 user_id。
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
	用户的 open_id。
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
        "event_type": "calendar.calendar.acl.created_v4",
        "create_time": "1608725989000",
        "token": "rvaYgkND1GOiu5MM0E1rncYC6PLtF7JV",
        "app_id": "cli_9f5343c580712544",
        "tenant_key": "2ca1d211f64f6438"
    },
    "event": {
        "acl_id": "user_xxxxx",
        "role": "unknown",
        "scope": {
            "type": "user",
            "user_id": {
                "union_id": "on_8ed6aa67826108097d9ee143816345",
                "user_id": "e33ggbyz",
                "open_id": "ou_84aad35d084aa403a838cf73ee18467"
            }
        },
        "user_id_list": [
            {
                "union_id": "on_xxxxxx",
                "user_id": "exxxxxxz",
                "open_id": "ou_xxxxxx"
            }
        ]
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
	"github.com/larksuite/oapi-sdk-go/v3/service/calendar/v4"
	larkws "github.com/larksuite/oapi-sdk-go/v3/ws"
)

// SDK 使用说明 SDK user guide：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
func main() {
	// 注册事件 Register event
	eventHandler := dispatcher.NewEventDispatcher("", "").
		OnP2CalendarAclCreatedV4(func(ctx context.Context, event *larkcalendar.P2CalendarAclCreatedV4) error {
			fmt.Printf("[ OnP2CalendarAclCreatedV4 access ], data: %s\n", larkcore.Prettify(event))
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


def do_p2_calendar_calendar_acl_created_v4(data: lark.calendar.v4.P2CalendarCalendarAclCreatedV4) -> None:
    print(f'[ do_p2_calendar_calendar_acl_created_v4 access ], data: {lark.JSON.marshal(data, indent=4)}')

# 注册事件 Register event
event_handler = lark.EventDispatcherHandler.builder("", "") \
    .register_p2_calendar_calendar_acl_created_v4(do_p2_calendar_calendar_acl_created_v4) \
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
import com.lark.oapi.service.calendar.CalendarService;
import com.lark.oapi.service.calendar.v4.model.P2CalendarAclCreatedV4;
import com.lark.oapi.event.EventDispatcher;
import com.lark.oapi.ws.Client;

// SDK 使用说明 SDK user guide：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
public class Sample {
    // 注册事件 Register event
    private static final EventDispatcher EVENT_HANDLER = EventDispatcher.newBuilder("", "")
            .onP2CalendarAclCreatedV4(new CalendarService.P2CalendarAclCreatedV4Handler() {
                @Override
                public void handle(P2CalendarAclCreatedV4 event) throws Exception {
                    System.out.printf("[ onP2CalendarAclCreatedV4 access ], data: %s\n", Jsons.DEFAULT.toJson(event.getEvent()));
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
        'calendar.calendar.acl.created_v4': async (data) => {
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
	"github.com/larksuite/oapi-sdk-go/v3/service/calendar/v4"
)

// SDK 使用说明 SDK user guide：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
func main() {
	// 注册事件 Register event
	eventHandler := dispatcher.NewEventDispatcher("", "").
		OnP2CalendarAclCreatedV4(func(ctx context.Context, event *larkcalendar.P2CalendarAclCreatedV4) error {
			fmt.Printf("[ OnP2CalendarAclCreatedV4 access ], data: %s\n", larkcore.Prettify(event))
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


def do_p2_calendar_calendar_acl_created_v4(data: lark.calendar.v4.P2CalendarCalendarAclCreatedV4) -> None:
    print(f'[ do_p2_calendar_calendar_acl_created_v4 access ], data: {lark.JSON.marshal(data, indent=4)}')

# 注册事件 Register event
event_handler = lark.EventDispatcherHandler.builder("", "") \
    .register_p2_calendar_calendar_acl_created_v4(do_p2_calendar_calendar_acl_created_v4) \
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
import com.lark.oapi.service.calendar.CalendarService;
import com.lark.oapi.service.calendar.v4.model.P2CalendarAclCreatedV4;
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
            .onP2CalendarAclCreatedV4(new CalendarService.P2CalendarAclCreatedV4Handler() {
                @Override
                public void handle(P2CalendarAclCreatedV4 event) throws Exception {
                    System.out.printf("[ onP2CalendarAclCreatedV4 access ], data: %s\n", Jsons.DEFAULT.toJson(event.getEvent()));
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
    'calendar.calendar.acl.created_v4': async (data) => {
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

