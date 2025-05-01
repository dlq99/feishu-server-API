# 流式更新 OpenAPI 调用指南
飞书卡片的流式更新能力是指飞书卡片的内容以实时或准实时的方式连续不断地更新，从而实现 AI 逐步生成、卡片逐步渲染的效果。在流式更新模式下，你可对卡片持续进行全量更新、局部更新、或文本流式更新操作。

卡片的流式更新能力和相关接口依赖卡片 JSON 2.0 结构。本文档介绍流式更新相关参数和使用步骤。

## 效果展示
以下为文本流式更新的效果展示：

| 快速上屏策略（默认） | 延迟上屏策略 |
| --- | --- |
| 调用流式更新文本接口后，若历史文本尚未流式上屏完毕，未上屏的部分将立即全部上屏，然后立即开始本次内容上屏：<br> <br><br><br> | 调用流式更新文本接口后，若历史文本尚未流式输出完毕，历史文本中未上屏部分将会继续按打字机效果输出直到全部输出完毕，再开始本次内容上屏：<br><br><br><br> |



## 注意事项

- 卡片流式更新模式开启期间，在用户交互卡片时，当服务端收到卡片的回调请求后，无法立即更新卡片。
- 要使用飞书卡片的流式更新能力和相关接口，你需要基于卡片 JSON 2.0 结构构造卡片。
- 卡片 JSON 2.0 结构支持飞书客户端 7.20 及之后版本。当使用 JSON 2.0 结构的卡片发送至低于 7.20 版本的客户端时，卡片标题可正常显示，但内容将展示兜底的升级提示文案。

  ![](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/35efb2f0bfbe5d22fe4b7a420925d2af_g5UivxGopO.png?height=449&lazyload=true&maxWidth=400&width=742)
- 在飞书 7.20 - 7.22 版本，流式更新功能使用默认的更新频率、步长和更新策略进行流式上屏。不支持指定参数。在飞书 7.23 及以上版本，流式更新功能支持指定参数，自定义频率、步长和策略。
- 默认参数可能根据客户端类型、版本、机型等因素存在差异。如果需要精确控制流式更新行为，建议手动指定流式参数。
- 为保证流式效果的一致性，卡片流式更新模式开启期间，建议前置指定流式更新参数，并保持整个流式更新过程中参数不变。

## 使用限制

- 对于单个租户下的单个应用，流式更新相关接口的调用频率上限为 1000 次/分，50 次/秒。
- 对于单个卡片实体的操作频率上限为 10 次/秒。
- 卡片实体的有效期为 14 天。即创建卡片实体超出 14 天后，你将无法调用相关接口操作卡片。
- 卡片实体支持的组件个数上限为 200。
- 卡片实体创建后，仅支持创建卡片实体的应用调用相关 OpenAPI 发送、操作卡片。
- 卡片在交互期间，无法实现流式更新。

## 流式效果配置

### JSON 结构

你可使用 `streaming_mode` 字段开启或关闭流式更新模式，使用 `streaming_config` 指定流式更新的频率、步长和更新策略。以下为流式更新功能支持配置的 JSON 字段：
```json
{
  "schema": "2.0",
  "config": {
    "streaming_mode": false, // 卡片是否处于流式更新模式，默认值为 false
    "streaming_config": {
      // 流式更新频率，单位：ms
      "print_frequency_ms": {
        "default": 30,
        "android": 25,
        "ios": 40,
        "pc": 50
      },
      // 流式更新步长，单位：字符数
      "print_step": {
        "default": 2,
        "android": 3,
        "ios": 4,
        "pc": 5
      },
      // 流式更新策略，枚举值，可取：fast/delay
      "print_strategy": "fast",
    }
  }
}
```

### 字段说明

现阶段，流式更新功能支持以下参数。
<md-dt-table>
<md-dt-thead>
<md-dt-tr>
<md-dt-th style="width: 40%;">字段名称</md-dt-th>
<md-dt-th style="width: 20%;">类型</md-dt-th>
<md-dt-th style="width: 10%;">必填</md-dt-th>
<md-dt-th style="width: 30%;">描述</md-dt-th>
</md-dt-tr>
</md-dt-thead>
<md-dt-tbody>
<md-dt-tr level="0">
<md-dt-td>
<md-text type="field-name" >streaming_mode
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >boolean
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
卡片是否处于流式更新模式。
</md-dt-td>
</md-dt-tr>

  
<md-dt-tr level="0">
<md-dt-td>
<md-text type="field-name" >streaming_config
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >object
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
流式更新参数配置。
</md-dt-td>
</md-dt-tr>
  
  
  
<md-dt-tr level="1">
<md-dt-td>
<md-text type="field-name" >print_frequency_ms
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >object
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
流式更新频率，即两次流式更新上屏之间的间隔时长。默认为 70 ms。支持分端配置。

**提示**：
- 若要配置三端统一的流式参数，仅指定 default 的值即可
- 若要为三端指定不同的流式参数，则在填写 default 参数的基础上，可选增加 Android/iOS/PC 三端的参数即可
</md-dt-td>
</md-dt-tr>

<md-dt-tr level="2">
<md-dt-td>
<md-text type="field-name" >default
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >number
</md-text>
</md-dt-td>
<md-dt-td>
是
</md-dt-td>
<md-dt-td>
三端通用统一频率
</md-dt-td>
</md-dt-tr>

<md-dt-tr level="2">
<md-dt-td>
<md-text type="field-name" >android
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >number
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
Android 端频率
</md-dt-td>
</md-dt-tr>

<md-dt-tr level="2">
<md-dt-td>
<md-text type="field-name" >ios
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >number
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
iOS 端频率
</md-dt-td>
</md-dt-tr>

<md-dt-tr level="2">
<md-dt-td>
<md-text type="field-name" >pc
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >number
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
pc 端频率
</md-dt-td>
</md-dt-tr>

<md-dt-tr level="1">
<md-dt-td>
<md-text type="field-name" >print_step
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >object
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
流式更新步长，即每次流式更新上屏打印的增量字符数。默认为 1。支持分端配置。
  
**提示**：
- 若要配置三端统一的流式参数，仅指定 default 的值即可
- 若要为三端指定不同的流式参数，则在填写 default 参数的基础上，可选增加Android/iOS/PC 三端的参数即可
</md-dt-td>
</md-dt-tr>

<md-dt-tr level="2">
<md-dt-td>
<md-text type="field-name" >default
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >number
</md-text>
</md-dt-td>
<md-dt-td>
是
</md-dt-td>
<md-dt-td>
三端通用步长
</md-dt-td>
</md-dt-tr>

<md-dt-tr level="2">
<md-dt-td>
<md-text type="field-name" >android
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >number
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
Android 端步长
</md-dt-td>
</md-dt-tr>

<md-dt-tr level="2">
<md-dt-td>
<md-text type="field-name" >ios
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >number
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
iOS 端步长
</md-dt-td>
</md-dt-tr>

<md-dt-tr level="2">
<md-dt-td>
<md-text type="field-name" >pc
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >number
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
PC 端步长
</md-dt-td>
</md-dt-tr>

<md-dt-tr level="1">
<md-dt-td>
<md-text type="field-name" >print_strategy
</md-text>
</md-dt-td>
<md-dt-td>
<md-text type="field-type" >enum
</md-text>
</md-dt-td>
<md-dt-td>
否
</md-dt-td>
<md-dt-td>
单个文本元素（tag 为 plain_text）或富文本组件内文本的流式更新策略，可选值如下所示，默认为 fast，即快速上屏。
  
- fast：快速上屏，为 7.20 - 7.22 版本的默认策略。调用流式更新文本接口后，若历史文本尚未流式上屏完毕，未上屏的部分将立即全部上屏，然后立即开始本次内容上屏
- delay：延迟上屏。调用流式更新文本接口后，若历史文本尚未流式输出完毕，历史文本中未上屏部分将会继续按打字机效果输出，直到全部输出完毕，再开始本次内容上屏
</md-dt-td>
</md-dt-tbody>
</md-dt-table>





> **📝 注意**
> 更多说明：
> 
> 假设某个富文本组件的内容是 **ABCDE**，当前 **ABC** 已上屏同时组件发生了更新，新文本是 **ABCDEFGH**。此时不同更新策略将产生不同的上屏效果：
> - 快速上屏：**ABCDE** 中没有上屏的 **DE** 会立刻上屏，组件直接展示 **ABCDE**；然后再按打字机效果上屏后续文本 **FGH**
> - 延迟上屏：**ABCDE** 中没有上屏的 **DE** 会按打字机效果依次上屏；然后再按打字机效果上屏后续文本**FGH**


## 快速入门

本小节介绍如何通过应用发送支持流式更新的飞书卡片，并实现文本级的流式更新效果。

### 前提条件

- 你已在飞书开发者后台](https://open.feishu.cn/app)创建了一个应用，并为应用添加了机器人能力、开通了以下权限。详情参考[创建并配置应用。
    - 以应用的身份发消息（im:message:send_as_bot）
    - 获取与发送单聊、群组消息（im:message）
    - 创建与更新卡片（cardkit:card:write）
- 你已基于卡片 JSON 2.0 结构构建了卡片 JSON。
- 你已按需设置了流式更新的频率、步长和策略，并将全局属性 `streaming_mode` 设置为 `true`，以开启卡片流式更新模式。以下为卡片 JSON 示例：
  ```json
  {
    "schema": "2.0",
    "header": {
      "title": {
        "content": "卡片标题",
        "tag": "plain_text"
      }
    },
    "config": {
      "streaming_mode": true, // 卡片是否处于流式更新模式，默认值为 false。
      "summary": {
        "content": "[生成中]" // 卡片在生成内容时展示的摘要。
      },
      "streaming_config": {
        // 流式更新频率，单位：ms
        "print_frequency_ms": {
          "default": 30,
          "android": 25,
          "ios": 40,
          "pc": 50
        },
        // 流式更新步长，单位：字符数
        "print_step": {
          "default": 2,
          "android": 3,
          "ios": 4,
          "pc": 5
        },
        // 流式更新策略，枚举值，可取：fast/delay
        "print_strategy": "fast",
      }
    },
    "body": {
      "elements": [
        {
          "tag": "markdown",
          "content": "卡片内容",
          "element_id": "markdown_1" // 操作组件的唯一标识。用于后续增加、删除组件等操作。该属性需在卡片全局唯一。
        }
      ]
    }
  }
  ```  
### 步骤一：调用创建卡片实体接口，获取卡片实体 ID

通过调用创建卡片实体接口，开启卡片的流式更新模式。同时获取卡片实体的 ID，用于发送卡片。Curl 示例如下所示。
- Mac 系统的 Curl 示例如下所示：
  ```bash
  curl --location --request POST 'https://open.feishu.cn/open-apis/cardkit/v1/cards/' \
  --header 'Authorization: Bearer t-g1025mfLWALKONCEVXRKJ32LN4DXK3ZQCHNabcef' \
  --header 'Content-Type: application/json; charset=utf-8' \
  --data-raw '{
    "type": "card_json",
    "data": "{\"schema\":\"2.0\",\"header\":{\"title\":{\"content\":\"卡片标题\",\"tag\":\"plain_text\"}},\"config\":{\"streaming_mode\":true,\"summary\":{\"content\":\"[生成中]\"}},\"body\":{\"elements\":[{\"tag\":\"markdown\",\"content\":\"卡片内容\",\"element_id\":\"markdown_1\"}]}}"
    }'
  ```
- Windows 系统的 Curl 示例如下所示：
  ```bash
  curl --location --request POST "https://open.feishu.cn/open-apis/cardkit/v1/cards/" ^
  --header "Authorization: Bearer t-g1025mfLWALKONCEVXRKJ32LN4DXK3ZQCHNabcef" ^
  --header "Content-Type: application/json; charset=utf-8" ^
  --data-raw "{\"type\": \"card_json\", \"data\": \"{\\\"schema\\\":\\\"2.0\\\",\\\"header\\\":{\\\"title\\\":{\\\"content\\\":\\\"卡片标题\\\",\\\"tag\\\":\\\"plain_text\\\"}},\\\"config\\\":{\\\"streaming_mode\\\":true,\\\"summary\\\":{\\\"content\\\":\\\"[生成中]\\\"}},\\\"body\\\":{\\\"elements\\\":[{\\\"tag\\\":\\\"markdown\\\",\\\"content\\\":\\\"卡片内容\\\",\\\"element_id\\\":\\\"markdown_1\\\"}]}}\"}"
  ```
调用成功将返回卡片实体 ID，同时为该卡片开启流式更新模式。流式更新模式将在距上次开启 10 分钟后自动关闭。你也可随时调用更新卡片配置API 将 `streaming_mode` 字段值设置为 false，以终止卡片的流式更新模式。

### 步骤二：发送卡片实体

参考发送消息接口文档，在请求体的 `content` 字段中传入卡片实体 ID，以发送卡片实体。


> **⚠️ 警告**
> **注意**
> - 卡片实体仅支持发送一次。
> - 发送卡片实体的应用必须是该卡片实体的创建应用。


发送卡片实体时，`content` 字段中的结构如下所示：
```json
{
    "type": "card",
    "data": {
        "card_id": "7371713483664506900"
    }
}
```
请求体示例如下所示：
```json
{
    // 与消息接收对象的 ID 类型（receive_id_type）一致的 ID 数据。例如用户 open_id 的值
    "receive_id": "ou_449b53ad6aee526f7ed311b216aabcef",
    // 发送消息的类型。卡片的类型值为：interactive
    "msg_type": "interactive",
    // 卡片实体 ID 结构序列化后的字符串
    "content": "{\"type\":\"card\",\"data\":{\"card_id\":\"7371713483664506900\"}}"
}
```
发送卡片实体的 Curl 命令如下所示。
- Mac 系统：
  ```bash
  curl -i -X POST 'https://open.feishu.cn/open-apis/im/v1/messages?receive_id_type=open_id' \
  -H 'Authorization: Bearer t-g1025mfLWALKONCEVXRKJ32LN4DXK3ZQCHNOYG4L' \
  -H 'Content-Type: application/json' \
  -d '{
          "content": "{\"type\":\"card\",\"data\":{\"card_id\":\"7371746107246182419\"}}",
          "msg_type": "interactive",
          "receive_id": "ou_31276d8e6626a2f98392b1d86c1abcef",
          "uuid": "a0d69e20-1dd1-458b-k525-dfeca4015205"
  }'
  ```
- Windows 系统：
  ```bash
  curl -i -X POST "https://open.feishu.cn/open-apis/im/v1/messages?receive_id_type=open_id" ^
  -H "Authorization: Bearer t-g1025mfLWALKONCEVXRKJ32LN4DXK3ZQCHNabcef" ^
  -H "Content-Type: application/json" ^
  -d "{\"content\": \"{\\\"type\\\":\\\"card\\\",\\\"data\\\":{\\\"card_id\\\":\\\"7371746107246182419\\\"}}\", \"msg_type\": \"interactive\", \"receive_id\": \"ou_31276d8e6626a2f98392b1d86c1abcef\", \"uuid\": \"a0d69e20-1dd1-458b-k525-dfeca4015205\"}"

  ```
成功返回的响应如下所示：
```json
{
    "code": 0,
    "data": {
        "body": {
            "content": "{\"title\":\"卡片标题\",\"elements\":[[]]}"
        },
        "chat_id": "oc_18f699eaf4cd495c64619c7c38aabcef",
        "create_time": "1716366350375",
        "deleted": false,
        "message_id": "om_32f44ef55e9b3fb5df74073f87835520",
        "msg_type": "interactive",
        "sender": {
            "id": "cli_a55fcc65b6babcef",
            "id_type": "app_id",
            "sender_type": "app",
            "tenant_key": "736588c9260abcef"
        },
        "update_time": "1716366350375",
        "updated": false
    },
    "msg": "success"
}
```

### 步骤三：流式更新文本

飞书卡片中的普通文本元素（tag 为 plain_text）和富文本组件支持对文本进行持续、增量的更新，从而实现“打字机”式的文字输出效果，提升终端用户体验。
卡片发送后，你可调用流式更新文本接口，对卡片中的普通文本元素（tag 为 plain_text）或富文本组件传入全量文本内容。若旧文本为传入的新文本的前缀子串，新增文本将在旧文本末尾继续以打字机效果输出；若新旧文本前缀不同，全量文本将直接上屏输出，无打字机效果。

Curl 命令如下所示：
- Mac 系统：
  ```bash
  curl --location --request PUT 'https://open.feishu.cn/open-apis/cardkit/v1/cards/7371746107246182419/elements/markdown_1/content' \
  --header 'Authorization: Bearer t-g1025mfLWALKONCEVXRKJ32LN4DXK3ZQCHNabcef' \
  --header 'Content-Type: application/json; charset=utf-8' \
  --data-raw '{
    "content": "这是更新后的文本内容。将以打字机式的效果输出",
    "sequence": 1708240925
  }'
  ```
- Windows 系统：
  ```bash
  curl --location --request PUT "https://open.feishu.cn/open-apis/cardkit/v1/cards/7371746107246182419/elements/markdown_1/content" ^
  --header "Authorization: Bearer t-g1025mfLWALKONCEVXRKJ32LN4DXK3ZQCHNabcef" ^
  --header "Content-Type: application/json; charset=utf-8" ^
  --data-raw "{\"content\": \"这是更新后的文本内容。将以打字机式的效果输出\", \"sequence\": 1708240925}"
  ```


## 常见问题

### Q: 流式卡片为什么在飞书客户端聊天栏消息预览中一直展示为[生成中]或者一个固定摘要文本，而不是实际卡片内容？

![image.png](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/a815e6bfd2b17a39a7f3f6dfc4d641fc_2767ux56oI.png?height=96&lazyload=true&maxWidth=400&width=591)
      
**[生成中]** 是卡片在流式模式过程中的默认摘要。这意味着卡片开启了流式更新模式。你需参考以下步骤关闭卡片的流式更新模式：

- 如果你基于搭建工具生成的卡片模板（template）的 ID 发送了卡片，你需在搭建工具中，点击右上角的设置按钮，关闭卡片的流式更新模式。
  
  
	![image.png](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/67c98d4db48485792e2bb7e19143d441_2cBen3yp7K.png?height=150&lazyload=true&maxWidth=400&width=650)
  
  
	![image.png](//sf3-cn.feishucdn.com/obj/open-platform-opendoc/bc3639696d417c8d3e7da3c4d4c70ba1_pfAJ3D1dGf.png?height=438&lazyload=true&maxWidth=400&width=642)
  
- 如果你基于卡片 JSON 发送了卡片，你需在卡片 JSON 中，将 `streaming_mode` 属性设为 `false`，关闭卡片的流式更新模式。
  

**提示**：生成中] 的摘要文本由卡片 JSON 中的 summary 属性控制。如果需要自定义摘要文本，调用[更新卡片配置接口自定义 summary 属性即可。

### Q: 流式卡片生成的卡片无法转发，如何解决？
      
开启了流式更新模式的卡片无法被转发。你需参考上文步骤关闭卡片的流式更新模式。
  

### Q: 流式卡片是否支持以交互更新的方式更新卡片？

支持，但是需要先关闭卡片的流式更新模式。流式更新模式将在距上次开启 10 分钟后自动关闭。你也可随时调用更新卡片配置 API 将 `streaming_mode` 字段值设置为 false 关闭流式。 
