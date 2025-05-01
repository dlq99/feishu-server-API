## 更新 OKR 进展记录

根据 OKR 进展记录 ID 更新进展详情。

## 请求

| 基本 | |
| --- | --- |
| HTTP URL | `https://open.feishu.cn/open-apis/okr/v1/progress_records/:progress_id` |
| HTTP Method | PUT |
| 支持的访问令牌 | tenant_access_token, user_access_token |
| 支持的应用类型 | custom |
| 权限要求 | 获取用户 user ID <br> 更新 OKR 信息 |
| 权限要求 | okr:okr |

### 路径参数

| 参数名 | 类型 |  描述 |
| ------ | ---- | ---- |
| progress_id | string | 待更新的 OKR进展记录 ID |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| user_id_type | string | 否 | 用户 ID 类型 |
### 请求体

| 参数名 | 类型 | 必填 | 描述 |
| ------ | ---- | ---- | ---- |
| content | object | 是 | 进展详情 富文本格式 <br> **示例**:   |

**类型额外说明**:

- **content_block** 类型说明:

  - **blocks** (array):
    - **content_block_element** 类型说明:

      基本属性:

       type: string <br>
      - **paragraph** (object):
        - **content_paragraph** 类型说明:

          - **style** (object):
            - **content_paragraph_style** 类型说明:

              - **list** (object):
                - **content_list** 类型说明:

                  基本属性:

                   type: string <br> indentLevel: integer <br> number: integer <br>
          - **elements** (array):
            - **content_paragraph_element** 类型说明:

              基本属性:

               type: string <br>
              - **textRun** (object):
                - **content_text_run** 类型说明:

                  基本属性:

                   text: string <br>
                  - **style** (object):
                    - **content_text_style** 类型说明:

                      基本属性:

                       bold: boolean <br> strikeThrough: boolean <br>
                      - **backColor** (object):
                        - **content_color** 类型说明:

                          基本属性:

                           red: integer <br> green: integer <br> blue: integer <br> alpha: number <br>
                      - **textColor** (object):
                        - **content_color** 类型说明:

                          基本属性:

                           red: integer <br> green: integer <br> blue: integer <br> alpha: number <br>
                      - **link** (object):
                        - **content_link** 类型说明:

                          基本属性:

                           url: string <br>
              - **docsLink** (object):
                - **content_docs_link** 类型说明:

                  基本属性:

                   url: string <br> title: string <br>
              - **person** (object):
                - **content_person** 类型说明:

                  基本属性:

                   openId: string <br>
      - **gallery** (object):
        - **content_gallery** 类型说明:

          - **imageList** (array):
            - **content_image_item** 类型说明:

              基本属性:

               fileToken: string <br> src: string <br> width: number <br> height: number <br>


**请求体示例**:

```json
{
    "content":{
        "blocks":[
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"粗体更新",
                                "style":{
                                    "bold":true
                                }
                            }
                        }
                    ]
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"*",
                                "style":{
                                    "bold":true
                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"删除线更新",
                                "style":{
                                    "strikeThrough":true
                                }
                            }
                        }
                    ]
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"字体颜色更新",
                                "style":{
                                    "textColor":{
                                        "red":216,
                                        "green":57,
                                        "blue":49,
                                        "alpha":1
                                    }
                                }
                            }
                        }
                    ]
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"背景颜色验证",
                                "style":{
                                    "backColor":{
                                        "red":251,
                                        "green":191,
                                        "blue":188,
                                        "alpha":1
                                    }
                                }
                            }
                        }
                    ]
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"粗体+删除+字体颜色+背景颜色验证",
                                "style":{
                                    "bold":true,
                                    "strikeThrough":true,
                                    "backColor":{
                                        "red":251,
                                        "green":191,
                                        "blue":188,
                                        "alpha":1
                                    },
                                    "textColor":{
                                        "red":216,
                                        "green":57,
                                        "blue":49,
                                        "alpha":1
                                    }
                                }
                            }
                        }
                    ]
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"有序标题1验证，",
                                "style":{

                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"粗体验证",
                                "style":{
                                    "bold":true
                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"number",
                            "indentLevel":1,
                            "number":1
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"有序标题2验证，",
                                "style":{

                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"删除线验证",
                                "style":{
                                    "strikeThrough":true
                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"number",
                            "indentLevel":1,
                            "number":2
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"有序标题3验证，",
                                "style":{

                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"字体背景颜色验证",
                                "style":{
                                    "backColor":{
                                        "red":251,
                                        "green":191,
                                        "blue":188,
                                        "alpha":1
                                    },
                                    "textColor":{
                                        "red":216,
                                        "green":57,
                                        "blue":49,
                                        "alpha":1
                                    }
                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"number",
                            "indentLevel":1,
                            "number":3
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"无序标题1验证，",
                                "style":{

                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"粗体",
                                "style":{
                                    "bold":true
                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"bullet",
                            "indentLevel":1
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"无序标题2验证，",
                                "style":{

                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"删除线",
                                "style":{
                                    "strikeThrough":true
                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"bullet",
                            "indentLevel":1
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"无序标题3验证，",
                                "style":{

                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"字体背景颜色验证",
                                "style":{
                                    "backColor":{
                                        "red":251,
                                        "green":191,
                                        "blue":188,
                                        "alpha":1
                                    },
                                    "textColor":{
                                        "red":216,
                                        "green":57,
                                        "blue":49,
                                        "alpha":1
                                    }
                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"bullet",
                            "indentLevel":1
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc",
                                "style":{
                                    "link":{
                                        "url":"https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc"
                                    }
                                }
                            }
                        }
                    ]
                }
            },
            {
                "type":"gallery",
                "gallery":{
                    "imageList":[
                        {
                            "src":"https://internal-api-okr.feishu-boe.cn/stream/api/downloadFile/?file_token=boxbcofrHwpgexwxyvgasR2kgRh&ticket=eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJ0YXJnZXRfaWQiOiI3MDQxNDMwMzc3NjQyMDgyMzIzIiwidGFyZ2V0X3R5cGUiOjMsImFjdGlvbiI6MiwiZmlsZV90b2tlbiI6ImJveGJjb2ZySHdwZ2V4d3h5dmdhc1Iya2dSaCIsInVzZXJfaWQiOiI2OTY5ODU1NTAxNzQ0ODM0MDkyIiwidGVuYW50X2lkIjoiNjg3NzUwMjY4NzYwOTQwNjk5MCIsImV4cCI6MTY0MDE1NjEyMX0.PSs94Z6ljo4e7U5cFV8dYW-bNDUOWdKXRK8B-XKruGCtKWrhsFLNKbNygUkOgHzbiPg65aSAiCaWyhh5YeX0aw",
                            "fileToken":"boxbcofrHwpgexwxyvgasR2kgRh",
                            "width":458,
                            "height":372
                        }
                    ]
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"任务列表未勾选验证",
                                "style":{

                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"checkBox",
                            "indentLevel":1
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"任务列表已勾选验证",
                                "style":{

                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"checkedBox",
                            "indentLevel":1
                        }
                    }
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
    "data": {
        "content": {
            "blocks": [
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {
                                        "bold": true
                                    },
                                    "text": "粗体更新"
                                },
                                "type": "textRun"
                            }
                        ]
                    },
                    "type": "paragraph"
                },
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {
                                        "bold": true
                                    },
                                    "text": "*"
                                },
                                "type": "textRun"
                            },
                            {
                                "textRun": {
                                    "style": {
                                        "strikeThrough": true
                                    },
                                    "text": "删除线更新"
                                },
                                "type": "textRun"
                            }
                        ]
                    },
                    "type": "paragraph"
                },
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {
                                        "textColor": {
                                            "alpha": 1,
                                            "blue": 49,
                                            "green": 57,
                                            "red": 216
                                        }
                                    },
                                    "text": "字体颜色更新"
                                },
                                "type": "textRun"
                            }
                        ]
                    },
                    "type": "paragraph"
                },
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {
                                        "backColor": {
                                            "alpha": 1,
                                            "blue": 188,
                                            "green": 191,
                                            "red": 251
                                        }
                                    },
                                    "text": "背景颜色验证"
                                },
                                "type": "textRun"
                            }
                        ]
                    },
                    "type": "paragraph"
                },
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {
                                        "backColor": {
                                            "alpha": 1,
                                            "blue": 188,
                                            "green": 191,
                                            "red": 251
                                        },
                                        "bold": true,
                                        "strikeThrough": true,
                                        "textColor": {
                                            "alpha": 1,
                                            "blue": 49,
                                            "green": 57,
                                            "red": 216
                                        }
                                    },
                                    "text": "粗体+删除+字体颜色+背景颜色验证"
                                },
                                "type": "textRun"
                            }
                        ]
                    },
                    "type": "paragraph"
                },
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {},
                                    "text": "有序标题1验证，"
                                },
                                "type": "textRun"
                            },
                            {
                                "textRun": {
                                    "style": {
                                        "bold": true
                                    },
                                    "text": "粗体验证"
                                },
                                "type": "textRun"
                            }
                        ],
                        "style": {
                            "list": {
                                "indentLevel": 1,
                                "number": 1,
                                "type": "number"
                            }
                        }
                    },
                    "type": "paragraph"
                },
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {},
                                    "text": "有序标题2验证，"
                                },
                                "type": "textRun"
                            },
                            {
                                "textRun": {
                                    "style": {
                                        "strikeThrough": true
                                    },
                                    "text": "删除线验证"
                                },
                                "type": "textRun"
                            }
                        ],
                        "style": {
                            "list": {
                                "indentLevel": 1,
                                "number": 2,
                                "type": "number"
                            }
                        }
                    },
                    "type": "paragraph"
                },
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {},
                                    "text": "有序标题3验证，"
                                },
                                "type": "textRun"
                            },
                            {
                                "textRun": {
                                    "style": {
                                        "backColor": {
                                            "alpha": 1,
                                            "blue": 188,
                                            "green": 191,
                                            "red": 251
                                        },
                                        "textColor": {
                                            "alpha": 1,
                                            "blue": 49,
                                            "green": 57,
                                            "red": 216
                                        }
                                    },
                                    "text": "字体背景颜色验证"
                                },
                                "type": "textRun"
                            }
                        ],
                        "style": {
                            "list": {
                                "indentLevel": 1,
                                "number": 3,
                                "type": "number"
                            }
                        }
                    },
                    "type": "paragraph"
                },
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {},
                                    "text": "无序标题1验证，"
                                },
                                "type": "textRun"
                            },
                            {
                                "textRun": {
                                    "style": {
                                        "bold": true
                                    },
                                    "text": "粗体"
                                },
                                "type": "textRun"
                            }
                        ],
                        "style": {
                            "list": {
                                "indentLevel": 1,
                                "type": "bullet"
                            }
                        }
                    },
                    "type": "paragraph"
                },
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {},
                                    "text": "无序标题2验证，"
                                },
                                "type": "textRun"
                            },
                            {
                                "textRun": {
                                    "style": {
                                        "strikeThrough": true
                                    },
                                    "text": "删除线"
                                },
                                "type": "textRun"
                            }
                        ],
                        "style": {
                            "list": {
                                "indentLevel": 1,
                                "type": "bullet"
                            }
                        }
                    },
                    "type": "paragraph"
                },
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {},
                                    "text": "无序标题3验证，"
                                },
                                "type": "textRun"
                            },
                            {
                                "textRun": {
                                    "style": {
                                        "backColor": {
                                            "alpha": 1,
                                            "blue": 188,
                                            "green": 191,
                                            "red": 251
                                        },
                                        "textColor": {
                                            "alpha": 1,
                                            "blue": 49,
                                            "green": 57,
                                            "red": 216
                                        }
                                    },
                                    "text": "字体背景颜色验证"
                                },
                                "type": "textRun"
                            }
                        ],
                        "style": {
                            "list": {
                                "indentLevel": 1,
                                "type": "bullet"
                            }
                        }
                    },
                    "type": "paragraph"
                },
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {
                                        "link": {
                                            "url": "https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc"
                                        }
                                    },
                                    "text": "https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc"
                                },
                                "type": "textRun"
                            }
                        ]
                    },
                    "type": "paragraph"
                },
                {
                    "gallery": {
                        "imageList": [
                            {
                                "fileToken": "boxbcofrHwpgexwxyvgasR2kgRh",
                                "height": 372,
                                "src": "https://internal-api-okr.feishu-boe.cn/stream/api/downloadFile/?file_token=boxbcofrHwpgexwxyvgasR2kgRh&ticket=eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJ0YXJnZXRfaWQiOiI3MDQxNDMwMzc3NjQyMDgyMzIzIiwidGFyZ2V0X3R5cGUiOjMsImFjdGlvbiI6MiwiZmlsZV90b2tlbiI6ImJveGJjb2ZySHdwZ2V4d3h5dmdhc1Iya2dSaCIsInVzZXJfaWQiOiI2OTY5ODU1NTAxNzQ0ODM0MDkyIiwidGVuYW50X2lkIjoiNjg3NzUwMjY4NzYwOTQwNjk5MCIsImV4cCI6MTY0MDE1NjEyMX0.PSs94Z6ljo4e7U5cFV8dYW-bNDUOWdKXRK8B-XKruGCtKWrhsFLNKbNygUkOgHzbiPg65aSAiCaWyhh5YeX0aw",
                                "width": 458
                            }
                        ]
                    },
                    "type": "gallery"
                },
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {},
                                    "text": "任务列表未勾选验证"
                                },
                                "type": "textRun"
                            }
                        ],
                        "style": {
                            "list": {
                                "indentLevel": 1,
                                "type": "checkBox"
                            }
                        }
                    },
                    "type": "paragraph"
                },
                {
                    "paragraph": {
                        "elements": [
                            {
                                "textRun": {
                                    "style": {},
                                    "text": "任务列表已勾选验证"
                                },
                                "type": "textRun"
                            }
                        ],
                        "style": {
                            "list": {
                                "indentLevel": 1,
                                "type": "checkedBox"
                            }
                        }
                    },
                    "type": "paragraph"
                }
            ]
        },
        "modify_time": "1640677887499",
        "progress_id": "7046518160811425812"
    },
    "msg": "success"
}
```

### 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
| ---------- | ------ | ---- | -------- |
| 500 | 1009999 | Unknown error. Please contact Feishu Assistant or your customer success manager. | 内部错误，请联系飞书助手或您的客户成功经理 |
| 500 | 1009998 | system exception | 系统异常 |
| 400 | 1001001 | Invalid parameters. Please check document and modify accordingly. | 无效的参数，请对照文档检查输入的参数 |
| 400 | 1001002 | No permission. | 您无权访问该接口，请确认您的登录凭证 |
| 400 | 1001003 | User not found. | 用户不存在 |
| 400 | 1001004 | OKR data not found. | 对应ID的数据不存在 |

### 调用示例

#### Python SDK

```python
import json

import lark_oapi as lark
from lark_oapi.api.okr.v1 import *


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
    request: UpdateProgressRecordRequest = UpdateProgressRecordRequest.builder() \
        .progress_id("7041857032248410131") \
        .user_id_type("open_id") \
        .request_body(UpdateProgressRecordRequestBody.builder()
            .content(ContentBlock.builder()
                .blocks([ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("粗体更新")
                                .style(ContentTextStyle.builder()
                                    .bold(True)
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("*")
                                .style(ContentTextStyle.builder()
                                    .bold(True)
                                    .build())
                                .build())
                            .build(), 
                            ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("删除线更新")
                                .style(ContentTextStyle.builder()
                                    .strike_through(True)
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("字体颜色更新")
                                .style(ContentTextStyle.builder()
                                    .text_color(ContentColor.builder()
                                        .red(216)
                                        .green(57)
                                        .blue(49)
                                        .alpha(1)
                                        .build())
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("背景颜色验证")
                                .style(ContentTextStyle.builder()
                                    .back_color(ContentColor.builder()
                                        .red(251)
                                        .green(191)
                                        .blue(188)
                                        .alpha(1)
                                        .build())
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("粗体+删除+字体颜色+背景颜色验证")
                                .style(ContentTextStyle.builder()
                                    .bold(True)
                                    .strike_through(True)
                                    .back_color(ContentColor.builder()
                                        .red(251)
                                        .green(191)
                                        .blue(188)
                                        .alpha(1)
                                        .build())
                                    .text_color(ContentColor.builder()
                                        .red(216)
                                        .green(57)
                                        .blue(49)
                                        .alpha(1)
                                        .build())
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .style(ContentParagraphStyle.builder()
                            .list(ContentList.builder()
                                .type("number")
                                .indent_level(1)
                                .number(1)
                                .build())
                            .build())
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("有序标题1验证，")
                                .style(ContentTextStyle.builder()
                                    .build())
                                .build())
                            .build(), 
                            ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("粗体验证")
                                .style(ContentTextStyle.builder()
                                    .bold(True)
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .style(ContentParagraphStyle.builder()
                            .list(ContentList.builder()
                                .type("number")
                                .indent_level(1)
                                .number(2)
                                .build())
                            .build())
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("有序标题2验证，")
                                .style(ContentTextStyle.builder()
                                    .build())
                                .build())
                            .build(), 
                            ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("删除线验证")
                                .style(ContentTextStyle.builder()
                                    .strike_through(True)
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .style(ContentParagraphStyle.builder()
                            .list(ContentList.builder()
                                .type("number")
                                .indent_level(1)
                                .number(3)
                                .build())
                            .build())
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("有序标题3验证，")
                                .style(ContentTextStyle.builder()
                                    .build())
                                .build())
                            .build(), 
                            ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("字体背景颜色验证")
                                .style(ContentTextStyle.builder()
                                    .back_color(ContentColor.builder()
                                        .red(251)
                                        .green(191)
                                        .blue(188)
                                        .alpha(1)
                                        .build())
                                    .text_color(ContentColor.builder()
                                        .red(216)
                                        .green(57)
                                        .blue(49)
                                        .alpha(1)
                                        .build())
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .style(ContentParagraphStyle.builder()
                            .list(ContentList.builder()
                                .type("bullet")
                                .indent_level(1)
                                .build())
                            .build())
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("无序标题1验证，")
                                .style(ContentTextStyle.builder()
                                    .build())
                                .build())
                            .build(), 
                            ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("粗体")
                                .style(ContentTextStyle.builder()
                                    .bold(True)
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .style(ContentParagraphStyle.builder()
                            .list(ContentList.builder()
                                .type("bullet")
                                .indent_level(1)
                                .build())
                            .build())
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("无序标题2验证，")
                                .style(ContentTextStyle.builder()
                                    .build())
                                .build())
                            .build(), 
                            ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("删除线")
                                .style(ContentTextStyle.builder()
                                    .strike_through(True)
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .style(ContentParagraphStyle.builder()
                            .list(ContentList.builder()
                                .type("bullet")
                                .indent_level(1)
                                .build())
                            .build())
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("无序标题3验证，")
                                .style(ContentTextStyle.builder()
                                    .build())
                                .build())
                            .build(), 
                            ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("字体背景颜色验证")
                                .style(ContentTextStyle.builder()
                                    .back_color(ContentColor.builder()
                                        .red(251)
                                        .green(191)
                                        .blue(188)
                                        .alpha(1)
                                        .build())
                                    .text_color(ContentColor.builder()
                                        .red(216)
                                        .green(57)
                                        .blue(49)
                                        .alpha(1)
                                        .build())
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc")
                                .style(ContentTextStyle.builder()
                                    .link(ContentLink.builder()
                                        .url("https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc")
                                        .build())
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("gallery")
                    .gallery(ContentGallery.builder()
                        .image_list([ContentImageItem.builder()
                            .file_token("boxbcofrHwpgexwxyvgasR2kgRh")
                            .src("https://internal-api-okr.feishu-boe.cn/stream/api/downloadFile/?file_token=boxbcofrHwpgexwxyvgasR2kgRh&ticket=eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJ0YXJnZXRfaWQiOiI3MDQxNDMwMzc3NjQyMDgyMzIzIiwidGFyZ2V0X3R5cGUiOjMsImFjdGlvbiI6MiwiZmlsZV90b2tlbiI6ImJveGJjb2ZySHdwZ2V4d3h5dmdhc1Iya2dSaCIsInVzZXJfaWQiOiI2OTY5ODU1NTAxNzQ0ODM0MDkyIiwidGVuYW50X2lkIjoiNjg3NzUwMjY4NzYwOTQwNjk5MCIsImV4cCI6MTY0MDE1NjEyMX0.PSs94Z6ljo4e7U5cFV8dYW-bNDUOWdKXRK8B-XKruGCtKWrhsFLNKbNygUkOgHzbiPg65aSAiCaWyhh5YeX0aw")
                            .width(458)
                            .height(372)
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .style(ContentParagraphStyle.builder()
                            .list(ContentList.builder()
                                .type("checkBox")
                                .indent_level(1)
                                .build())
                            .build())
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("任务列表未勾选验证")
                                .style(ContentTextStyle.builder()
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build(), 
                    ContentBlockElement.builder()
                    .type("paragraph")
                    .paragraph(ContentParagraph.builder()
                        .style(ContentParagraphStyle.builder()
                            .list(ContentList.builder()
                                .type("checkedBox")
                                .indent_level(1)
                                .build())
                            .build())
                        .elements([ContentParagraphElement.builder()
                            .type("textRun")
                            .text_run(ContentTextRun.builder()
                                .text("任务列表已勾选验证")
                                .style(ContentTextStyle.builder()
                                    .build())
                                .build())
                            .build()
                            ])
                        .build())
                    .build()
                    ])
                .build())
            .build()) \
        .build()

    # 发起请求
    response: UpdateProgressRecordResponse = client.okr.v1.progress_record.update(request)

    # 处理失败返回
    if not response.success():
        lark.logger.error(
            f"client.okr.v1.progress_record.update failed, code: {response.code}, msg: {response.msg}, log_id: {response.get_log_id()}, resp: \n{json.dumps(json.loads(response.raw.content), indent=4, ensure_ascii=False)}")
        return

    # 处理业务结果
    lark.logger.info(lark.JSON.marshal(response.data, indent=4))


if __name__ == "__main__":
    main()

```

#### Java SDK

```java
package com.lark.oapi.sample.apiall.okrv1;
import com.google.gson.JsonParser;
import com.lark.oapi.Client;
import com.lark.oapi.core.utils.Jsons;
import com.lark.oapi.service.okr.v1.model.*;
import java.util.HashMap;
import com.lark.oapi.core.request.RequestOptions;

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/java-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
public class UpdateProgressRecordSample{

  public static void main(String arg[]) throws Exception {
      // 构建client
      Client client = Client.newBuilder("YOUR_APP_ID", "YOUR_APP_SECRET").build();

      // 创建请求对象
      UpdateProgressRecordReq req = UpdateProgressRecordReq.newBuilder()
             .progressId("7041857032248410131")
             .userIdType("open_id")
             .updateProgressRecordReqBody(UpdateProgressRecordReqBody.newBuilder()
                 .content(ContentBlock.newBuilder()
                        .blocks(new ContentBlockElement[]{
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("粗体更新")
                                .style(ContentTextStyle.newBuilder()
                                  .bold(true)
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("*")
                                .style(ContentTextStyle.newBuilder()
                                  .bold(true)
                                  .build())
                                .build())
                              .build(),
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("删除线更新")
                                .style(ContentTextStyle.newBuilder()
                                  .strikeThrough(true)
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("字体颜色更新")
                                .style(ContentTextStyle.newBuilder()
                                  .textColor(ContentColor.newBuilder()
                                    .red(216)
                                    .green(57)
                                    .blue(49)
                                    .alpha(1)
                                    .build())
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("背景颜色验证")
                                .style(ContentTextStyle.newBuilder()
                                  .backColor(ContentColor.newBuilder()
                                    .red(251)
                                    .green(191)
                                    .blue(188)
                                    .alpha(1)
                                    .build())
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("粗体+删除+字体颜色+背景颜色验证")
                                .style(ContentTextStyle.newBuilder()
                                  .bold(true)
                                  .strikeThrough(true)
                                  .backColor(ContentColor.newBuilder()
                                    .red(251)
                                    .green(191)
                                    .blue(188)
                                    .alpha(1)
                                    .build())
                                  .textColor(ContentColor.newBuilder()
                                    .red(216)
                                    .green(57)
                                    .blue(49)
                                    .alpha(1)
                                    .build())
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .style(ContentParagraphStyle.newBuilder()
                              .list(ContentList.newBuilder()
                                .type("number")
                                .indentLevel(1)
                                .number(1)
                                .build())
                              .build())
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("有序标题1验证，")
                                .style(ContentTextStyle.newBuilder()
                                  .build())
                                .build())
                              .build(),
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("粗体验证")
                                .style(ContentTextStyle.newBuilder()
                                  .bold(true)
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .style(ContentParagraphStyle.newBuilder()
                              .list(ContentList.newBuilder()
                                .type("number")
                                .indentLevel(1)
                                .number(2)
                                .build())
                              .build())
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("有序标题2验证，")
                                .style(ContentTextStyle.newBuilder()
                                  .build())
                                .build())
                              .build(),
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("删除线验证")
                                .style(ContentTextStyle.newBuilder()
                                  .strikeThrough(true)
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .style(ContentParagraphStyle.newBuilder()
                              .list(ContentList.newBuilder()
                                .type("number")
                                .indentLevel(1)
                                .number(3)
                                .build())
                              .build())
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("有序标题3验证，")
                                .style(ContentTextStyle.newBuilder()
                                  .build())
                                .build())
                              .build(),
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("字体背景颜色验证")
                                .style(ContentTextStyle.newBuilder()
                                  .backColor(ContentColor.newBuilder()
                                    .red(251)
                                    .green(191)
                                    .blue(188)
                                    .alpha(1)
                                    .build())
                                  .textColor(ContentColor.newBuilder()
                                    .red(216)
                                    .green(57)
                                    .blue(49)
                                    .alpha(1)
                                    .build())
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .style(ContentParagraphStyle.newBuilder()
                              .list(ContentList.newBuilder()
                                .type("bullet")
                                .indentLevel(1)
                                .build())
                              .build())
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("无序标题1验证，")
                                .style(ContentTextStyle.newBuilder()
                                  .build())
                                .build())
                              .build(),
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("粗体")
                                .style(ContentTextStyle.newBuilder()
                                  .bold(true)
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .style(ContentParagraphStyle.newBuilder()
                              .list(ContentList.newBuilder()
                                .type("bullet")
                                .indentLevel(1)
                                .build())
                              .build())
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("无序标题2验证，")
                                .style(ContentTextStyle.newBuilder()
                                  .build())
                                .build())
                              .build(),
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("删除线")
                                .style(ContentTextStyle.newBuilder()
                                  .strikeThrough(true)
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .style(ContentParagraphStyle.newBuilder()
                              .list(ContentList.newBuilder()
                                .type("bullet")
                                .indentLevel(1)
                                .build())
                              .build())
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("无序标题3验证，")
                                .style(ContentTextStyle.newBuilder()
                                  .build())
                                .build())
                              .build(),
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("字体背景颜色验证")
                                .style(ContentTextStyle.newBuilder()
                                  .backColor(ContentColor.newBuilder()
                                    .red(251)
                                    .green(191)
                                    .blue(188)
                                    .alpha(1)
                                    .build())
                                  .textColor(ContentColor.newBuilder()
                                    .red(216)
                                    .green(57)
                                    .blue(49)
                                    .alpha(1)
                                    .build())
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc")
                                .style(ContentTextStyle.newBuilder()
                                  .link(ContentLink.newBuilder()
                                    .url("https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc")
                                    .build())
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("gallery")
                          .gallery(ContentGallery.newBuilder()
                            .imageList(new ContentImageItem[]{
                            ContentImageItem.newBuilder()
                              .fileToken("boxbcofrHwpgexwxyvgasR2kgRh")
                              .src("https://internal-api-okr.feishu-boe.cn/stream/api/downloadFile/?file_token=boxbcofrHwpgexwxyvgasR2kgRh&ticket=eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJ0YXJnZXRfaWQiOiI3MDQxNDMwMzc3NjQyMDgyMzIzIiwidGFyZ2V0X3R5cGUiOjMsImFjdGlvbiI6MiwiZmlsZV90b2tlbiI6ImJveGJjb2ZySHdwZ2V4d3h5dmdhc1Iya2dSaCIsInVzZXJfaWQiOiI2OTY5ODU1NTAxNzQ0ODM0MDkyIiwidGVuYW50X2lkIjoiNjg3NzUwMjY4NzYwOTQwNjk5MCIsImV4cCI6MTY0MDE1NjEyMX0.PSs94Z6ljo4e7U5cFV8dYW-bNDUOWdKXRK8B-XKruGCtKWrhsFLNKbNygUkOgHzbiPg65aSAiCaWyhh5YeX0aw")
                              .width(458)
                              .height(372)
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .style(ContentParagraphStyle.newBuilder()
                              .list(ContentList.newBuilder()
                                .type("checkBox")
                                .indentLevel(1)
                                .build())
                              .build())
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("任务列表未勾选验证")
                                .style(ContentTextStyle.newBuilder()
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build(),
                        ContentBlockElement.newBuilder()
                          .type("paragraph")
                          .paragraph(ContentParagraph.newBuilder()
                            .style(ContentParagraphStyle.newBuilder()
                              .list(ContentList.newBuilder()
                                .type("checkedBox")
                                .indentLevel(1)
                                .build())
                              .build())
                            .elements(new ContentParagraphElement[]{
                            ContentParagraphElement.newBuilder()
                              .type("textRun")
                              .textRun(ContentTextRun.newBuilder()
                                .text("任务列表已勾选验证")
                                .style(ContentTextStyle.newBuilder()
                                  .build())
                                .build())
                              .build()
                            })
                            .build())
                          .build()
                        })
                        .build())
                  .build())
             .build();

      // 发起请求
      UpdateProgressRecordResp resp = client.okr().v1().progressRecord().update(req);

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

client.okr.v1.progressRecord.update({
        path: {
                progress_id:'7041857032248410131',
        },
        params: {
                user_id_type:'open_id',
        },
        data: {
                content:{
                        blocks:[
                        {
                          type:'paragraph',
                          paragraph:{
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'粗体更新',
                                style:{
                                  bold:true,
                                  },
                                },
                              }
                            ],
                            },
                          },
                        {
                          type:'paragraph',
                          paragraph:{
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'*',
                                style:{
                                  bold:true,
                                  },
                                },
                              },
                            {
                              type:'textRun',
                              textRun:{
                                text:'删除线更新',
                                style:{
                                  strikeThrough:true,
                                  },
                                },
                              }
                            ],
                            },
                          },
                        {
                          type:'paragraph',
                          paragraph:{
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'字体颜色更新',
                                style:{
                                  textColor:{
                                    red:216,
                                    green:57,
                                    blue:49,
                                    alpha:1,
                                    },
                                  },
                                },
                              }
                            ],
                            },
                          },
                        {
                          type:'paragraph',
                          paragraph:{
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'背景颜色验证',
                                style:{
                                  backColor:{
                                    red:251,
                                    green:191,
                                    blue:188,
                                    alpha:1,
                                    },
                                  },
                                },
                              }
                            ],
                            },
                          },
                        {
                          type:'paragraph',
                          paragraph:{
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'粗体+删除+字体颜色+背景颜色验证',
                                style:{
                                  bold:true,
                                  strikeThrough:true,
                                  backColor:{
                                    red:251,
                                    green:191,
                                    blue:188,
                                    alpha:1,
                                    },
                                  textColor:{
                                    red:216,
                                    green:57,
                                    blue:49,
                                    alpha:1,
                                    },
                                  },
                                },
                              }
                            ],
                            },
                          },
                        {
                          type:'paragraph',
                          paragraph:{
                            style:{
                              list:{
                                type:'number',
                                indentLevel:1,
                                number:1,
                                },
                              },
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'有序标题1验证，',
                                style:{
                                  },
                                },
                              },
                            {
                              type:'textRun',
                              textRun:{
                                text:'粗体验证',
                                style:{
                                  bold:true,
                                  },
                                },
                              }
                            ],
                            },
                          },
                        {
                          type:'paragraph',
                          paragraph:{
                            style:{
                              list:{
                                type:'number',
                                indentLevel:1,
                                number:2,
                                },
                              },
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'有序标题2验证，',
                                style:{
                                  },
                                },
                              },
                            {
                              type:'textRun',
                              textRun:{
                                text:'删除线验证',
                                style:{
                                  strikeThrough:true,
                                  },
                                },
                              }
                            ],
                            },
                          },
                        {
                          type:'paragraph',
                          paragraph:{
                            style:{
                              list:{
                                type:'number',
                                indentLevel:1,
                                number:3,
                                },
                              },
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'有序标题3验证，',
                                style:{
                                  },
                                },
                              },
                            {
                              type:'textRun',
                              textRun:{
                                text:'字体背景颜色验证',
                                style:{
                                  backColor:{
                                    red:251,
                                    green:191,
                                    blue:188,
                                    alpha:1,
                                    },
                                  textColor:{
                                    red:216,
                                    green:57,
                                    blue:49,
                                    alpha:1,
                                    },
                                  },
                                },
                              }
                            ],
                            },
                          },
                        {
                          type:'paragraph',
                          paragraph:{
                            style:{
                              list:{
                                type:'bullet',
                                indentLevel:1,
                                },
                              },
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'无序标题1验证，',
                                style:{
                                  },
                                },
                              },
                            {
                              type:'textRun',
                              textRun:{
                                text:'粗体',
                                style:{
                                  bold:true,
                                  },
                                },
                              }
                            ],
                            },
                          },
                        {
                          type:'paragraph',
                          paragraph:{
                            style:{
                              list:{
                                type:'bullet',
                                indentLevel:1,
                                },
                              },
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'无序标题2验证，',
                                style:{
                                  },
                                },
                              },
                            {
                              type:'textRun',
                              textRun:{
                                text:'删除线',
                                style:{
                                  strikeThrough:true,
                                  },
                                },
                              }
                            ],
                            },
                          },
                        {
                          type:'paragraph',
                          paragraph:{
                            style:{
                              list:{
                                type:'bullet',
                                indentLevel:1,
                                },
                              },
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'无序标题3验证，',
                                style:{
                                  },
                                },
                              },
                            {
                              type:'textRun',
                              textRun:{
                                text:'字体背景颜色验证',
                                style:{
                                  backColor:{
                                    red:251,
                                    green:191,
                                    blue:188,
                                    alpha:1,
                                    },
                                  textColor:{
                                    red:216,
                                    green:57,
                                    blue:49,
                                    alpha:1,
                                    },
                                  },
                                },
                              }
                            ],
                            },
                          },
                        {
                          type:'paragraph',
                          paragraph:{
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc',
                                style:{
                                  link:{
                                    url:'https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc',
                                    },
                                  },
                                },
                              }
                            ],
                            },
                          },
                        {
                          type:'gallery',
                          gallery:{
                            imageList:[
                            {
                              fileToken:'boxbcofrHwpgexwxyvgasR2kgRh',
                              src:'https://internal-api-okr.feishu-boe.cn/stream/api/downloadFile/?file_token=boxbcofrHwpgexwxyvgasR2kgRh&ticket=eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJ0YXJnZXRfaWQiOiI3MDQxNDMwMzc3NjQyMDgyMzIzIiwidGFyZ2V0X3R5cGUiOjMsImFjdGlvbiI6MiwiZmlsZV90b2tlbiI6ImJveGJjb2ZySHdwZ2V4d3h5dmdhc1Iya2dSaCIsInVzZXJfaWQiOiI2OTY5ODU1NTAxNzQ0ODM0MDkyIiwidGVuYW50X2lkIjoiNjg3NzUwMjY4NzYwOTQwNjk5MCIsImV4cCI6MTY0MDE1NjEyMX0.PSs94Z6ljo4e7U5cFV8dYW-bNDUOWdKXRK8B-XKruGCtKWrhsFLNKbNygUkOgHzbiPg65aSAiCaWyhh5YeX0aw',
                              width:458,
                              height:372,
                              }
                            ],
                            },
                          },
                        {
                          type:'paragraph',
                          paragraph:{
                            style:{
                              list:{
                                type:'checkBox',
                                indentLevel:1,
                                },
                              },
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'任务列表未勾选验证',
                                style:{
                                  },
                                },
                              }
                            ],
                            },
                          },
                        {
                          type:'paragraph',
                          paragraph:{
                            style:{
                              list:{
                                type:'checkedBox',
                                indentLevel:1,
                                },
                              },
                            elements:[
                            {
                              type:'textRun',
                              textRun:{
                                text:'任务列表已勾选验证',
                                style:{
                                  },
                                },
                              }
                            ],
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
var client = new RestClient("https://open.feishu.cn/open-apis/okr/v1/progress_records/7041857032248410131?user_id_type=open_id");
client.Timeout = -1;
var request = new RestRequest(Method.PUT);
request.AddHeader("Authorization", "Bearer t-7f1b******8e560");
request.AddHeader("Content-Type", "application/json");
var body = "{\"content\":{\"blocks\":[{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{\"bold\":true},\"text\":\"粗体更新\"},\"type\":\"textRun\"}]},\"type\":\"paragraph\"},{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{\"bold\":true},\"text\":\"*\"},\"type\":\"textRun\"},{\"textRun\":{\"style\":{\"strikeThrough\":true},\"text\":\"删除线更新\"},\"type\":\"textRun\"}]},\"type\":\"paragraph\"},{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{\"textColor\":{\"alpha\":1,\"blue\":49,\"green\":57,\"red\":216}},\"text\":\"字体颜色更新\"},\"type\":\"textRun\"}]},\"type\":\"paragraph\"},{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{\"backColor\":{\"alpha\":1,\"blue\":188,\"green\":191,\"red\":251}},\"text\":\"背景颜色验证\"},\"type\":\"textRun\"}]},\"type\":\"paragraph\"},{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{\"backColor\":{\"alpha\":1,\"blue\":188,\"green\":191,\"red\":251},\"bold\":true,\"strikeThrough\":true,\"textColor\":{\"alpha\":1,\"blue\":49,\"green\":57,\"red\":216}},\"text\":\"粗体+删除+字体颜色+背景颜色验证\"},\"type\":\"textRun\"}]},\"type\":\"paragraph\"},{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{},\"text\":\"有序标题1验证，\"},\"type\":\"textRun\"},{\"textRun\":{\"style\":{\"bold\":true},\"text\":\"粗体验证\"},\"type\":\"textRun\"}],\"style\":{\"list\":{\"indentLevel\":1,\"number\":1,\"type\":\"number\"}}},\"type\":\"paragraph\"},{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{},\"text\":\"有序标题2验证，\"},\"type\":\"textRun\"},{\"textRun\":{\"style\":{\"strikeThrough\":true},\"text\":\"删除线验证\"},\"type\":\"textRun\"}],\"style\":{\"list\":{\"indentLevel\":1,\"number\":2,\"type\":\"number\"}}},\"type\":\"paragraph\"},{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{},\"text\":\"有序标题3验证，\"},\"type\":\"textRun\"},{\"textRun\":{\"style\":{\"backColor\":{\"alpha\":1,\"blue\":188,\"green\":191,\"red\":251},\"textColor\":{\"alpha\":1,\"blue\":49,\"green\":57,\"red\":216}},\"text\":\"字体背景颜色验证\"},\"type\":\"textRun\"}],\"style\":{\"list\":{\"indentLevel\":1,\"number\":3,\"type\":\"number\"}}},\"type\":\"paragraph\"},{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{},\"text\":\"无序标题1验证，\"},\"type\":\"textRun\"},{\"textRun\":{\"style\":{\"bold\":true},\"text\":\"粗体\"},\"type\":\"textRun\"}],\"style\":{\"list\":{\"indentLevel\":1,\"type\":\"bullet\"}}},\"type\":\"paragraph\"},{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{},\"text\":\"无序标题2验证，\"},\"type\":\"textRun\"},{\"textRun\":{\"style\":{\"strikeThrough\":true},\"text\":\"删除线\"},\"type\":\"textRun\"}],\"style\":{\"list\":{\"indentLevel\":1,\"type\":\"bullet\"}}},\"type\":\"paragraph\"},{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{},\"text\":\"无序标题3验证，\"},\"type\":\"textRun\"},{\"textRun\":{\"style\":{\"backColor\":{\"alpha\":1,\"blue\":188,\"green\":191,\"red\":251},\"textColor\":{\"alpha\":1,\"blue\":49,\"green\":57,\"red\":216}},\"text\":\"字体背景颜色验证\"},\"type\":\"textRun\"}],\"style\":{\"list\":{\"indentLevel\":1,\"type\":\"bullet\"}}},\"type\":\"paragraph\"},{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{\"link\":{\"url\":\"https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc\"}},\"text\":\"https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc\"},\"type\":\"textRun\"}]},\"type\":\"paragraph\"},{\"gallery\":{\"imageList\":[{\"fileToken\":\"boxbcofrHwpgexwxyvgasR2kgRh\",\"height\":372,\"src\":\"https://internal-api-okr.feishu-boe.cn/stream/api/downloadFile/?file_token=boxbcofrHwpgexwxyvgasR2kgRh&ticket=eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJ0YXJnZXRfaWQiOiI3MDQxNDMwMzc3NjQyMDgyMzIzIiwidGFyZ2V0X3R5cGUiOjMsImFjdGlvbiI6MiwiZmlsZV90b2tlbiI6ImJveGJjb2ZySHdwZ2V4d3h5dmdhc1Iya2dSaCIsInVzZXJfaWQiOiI2OTY5ODU1NTAxNzQ0ODM0MDkyIiwidGVuYW50X2lkIjoiNjg3NzUwMjY4NzYwOTQwNjk5MCIsImV4cCI6MTY0MDE1NjEyMX0.PSs94Z6ljo4e7U5cFV8dYW-bNDUOWdKXRK8B-XKruGCtKWrhsFLNKbNygUkOgHzbiPg65aSAiCaWyhh5YeX0aw\",\"width\":458}]},\"type\":\"gallery\"},{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{},\"text\":\"任务列表未勾选验证\"},\"type\":\"textRun\"}],\"style\":{\"list\":{\"indentLevel\":1,\"type\":\"checkBox\"}}},\"type\":\"paragraph\"},{\"paragraph\":{\"elements\":[{\"textRun\":{\"style\":{},\"text\":\"任务列表已勾选验证\"},\"type\":\"textRun\"}],\"style\":{\"list\":{\"indentLevel\":1,\"type\":\"checkedBox\"}}},\"type\":\"paragraph\"}]}}";
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
    "content":{
        "blocks":[
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"粗体更新",
                                "style":{
                                    "bold":true
                                }
                            }
                        }
                    ]
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"*",
                                "style":{
                                    "bold":true
                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"删除线更新",
                                "style":{
                                    "strikeThrough":true
                                }
                            }
                        }
                    ]
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"字体颜色更新",
                                "style":{
                                    "textColor":{
                                        "red":216,
                                        "green":57,
                                        "blue":49,
                                        "alpha":1
                                    }
                                }
                            }
                        }
                    ]
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"背景颜色验证",
                                "style":{
                                    "backColor":{
                                        "red":251,
                                        "green":191,
                                        "blue":188,
                                        "alpha":1
                                    }
                                }
                            }
                        }
                    ]
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"粗体+删除+字体颜色+背景颜色验证",
                                "style":{
                                    "bold":true,
                                    "strikeThrough":true,
                                    "backColor":{
                                        "red":251,
                                        "green":191,
                                        "blue":188,
                                        "alpha":1
                                    },
                                    "textColor":{
                                        "red":216,
                                        "green":57,
                                        "blue":49,
                                        "alpha":1
                                    }
                                }
                            }
                        }
                    ]
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"有序标题1验证，",
                                "style":{

                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"粗体验证",
                                "style":{
                                    "bold":true
                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"number",
                            "indentLevel":1,
                            "number":1
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"有序标题2验证，",
                                "style":{

                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"删除线验证",
                                "style":{
                                    "strikeThrough":true
                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"number",
                            "indentLevel":1,
                            "number":2
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"有序标题3验证，",
                                "style":{

                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"字体背景颜色验证",
                                "style":{
                                    "backColor":{
                                        "red":251,
                                        "green":191,
                                        "blue":188,
                                        "alpha":1
                                    },
                                    "textColor":{
                                        "red":216,
                                        "green":57,
                                        "blue":49,
                                        "alpha":1
                                    }
                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"number",
                            "indentLevel":1,
                            "number":3
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"无序标题1验证，",
                                "style":{

                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"粗体",
                                "style":{
                                    "bold":true
                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"bullet",
                            "indentLevel":1
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"无序标题2验证，",
                                "style":{

                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"删除线",
                                "style":{
                                    "strikeThrough":true
                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"bullet",
                            "indentLevel":1
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"无序标题3验证，",
                                "style":{

                                }
                            }
                        },
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"字体背景颜色验证",
                                "style":{
                                    "backColor":{
                                        "red":251,
                                        "green":191,
                                        "blue":188,
                                        "alpha":1
                                    },
                                    "textColor":{
                                        "red":216,
                                        "green":57,
                                        "blue":49,
                                        "alpha":1
                                    }
                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"bullet",
                            "indentLevel":1
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc",
                                "style":{
                                    "link":{
                                        "url":"https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc"
                                    }
                                }
                            }
                        }
                    ]
                }
            },
            {
                "type":"gallery",
                "gallery":{
                    "imageList":[
                        {
                            "src":"https://internal-api-okr.feishu-boe.cn/stream/api/downloadFile/?file_token=boxbcofrHwpgexwxyvgasR2kgRh&ticket=eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJ0YXJnZXRfaWQiOiI3MDQxNDMwMzc3NjQyMDgyMzIzIiwidGFyZ2V0X3R5cGUiOjMsImFjdGlvbiI6MiwiZmlsZV90b2tlbiI6ImJveGJjb2ZySHdwZ2V4d3h5dmdhc1Iya2dSaCIsInVzZXJfaWQiOiI2OTY5ODU1NTAxNzQ0ODM0MDkyIiwidGVuYW50X2lkIjoiNjg3NzUwMjY4NzYwOTQwNjk5MCIsImV4cCI6MTY0MDE1NjEyMX0.PSs94Z6ljo4e7U5cFV8dYW-bNDUOWdKXRK8B-XKruGCtKWrhsFLNKbNygUkOgHzbiPg65aSAiCaWyhh5YeX0aw",
                            "fileToken":"boxbcofrHwpgexwxyvgasR2kgRh",
                            "width":458,
                            "height":372
                        }
                    ]
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"任务列表未勾选验证",
                                "style":{

                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"checkBox",
                            "indentLevel":1
                        }
                    }
                }
            },
            {
                "type":"paragraph",
                "paragraph":{
                    "elements":[
                        {
                            "type":"textRun",
                            "textRun":{
                                "text":"任务列表已勾选验证",
                                "style":{

                                }
                            }
                        }
                    ],
                    "style":{
                        "list":{
                            "type":"checkedBox",
                            "indentLevel":1
                        }
                    }
                }
            }
        ]
    }
}';
$request = new Request('PUT', 'https://open.feishu.cn/open-apis/okr/v1/progress_records/7041857032248410131?user_id_type=open_id', $headers, $body);
$res = $client->sendAsync($request)->wait();
echo $res->getBody();
```

#### Curl

```bash
curl -i -X PUT 'https://open.feishu.cn/open-apis/okr/v1/progress_records/7041857032248410131?user_id_type=open_id' \
-H 'Authorization: Bearer t-7f1b******8e560' \
-H 'Content-Type: application/json' \
-d '{
	"content": {
		"blocks": [
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {
									"bold": true
								},
								"text": "粗体更新"
							},
							"type": "textRun"
						}
					]
				},
				"type": "paragraph"
			},
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {
									"bold": true
								},
								"text": "*"
							},
							"type": "textRun"
						},
						{
							"textRun": {
								"style": {
									"strikeThrough": true
								},
								"text": "删除线更新"
							},
							"type": "textRun"
						}
					]
				},
				"type": "paragraph"
			},
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {
									"textColor": {
										"alpha": 1,
										"blue": 49,
										"green": 57,
										"red": 216
									}
								},
								"text": "字体颜色更新"
							},
							"type": "textRun"
						}
					]
				},
				"type": "paragraph"
			},
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {
									"backColor": {
										"alpha": 1,
										"blue": 188,
										"green": 191,
										"red": 251
									}
								},
								"text": "背景颜色验证"
							},
							"type": "textRun"
						}
					]
				},
				"type": "paragraph"
			},
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {
									"backColor": {
										"alpha": 1,
										"blue": 188,
										"green": 191,
										"red": 251
									},
									"bold": true,
									"strikeThrough": true,
									"textColor": {
										"alpha": 1,
										"blue": 49,
										"green": 57,
										"red": 216
									}
								},
								"text": "粗体+删除+字体颜色+背景颜色验证"
							},
							"type": "textRun"
						}
					]
				},
				"type": "paragraph"
			},
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {},
								"text": "有序标题1验证，"
							},
							"type": "textRun"
						},
						{
							"textRun": {
								"style": {
									"bold": true
								},
								"text": "粗体验证"
							},
							"type": "textRun"
						}
					],
					"style": {
						"list": {
							"indentLevel": 1,
							"number": 1,
							"type": "number"
						}
					}
				},
				"type": "paragraph"
			},
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {},
								"text": "有序标题2验证，"
							},
							"type": "textRun"
						},
						{
							"textRun": {
								"style": {
									"strikeThrough": true
								},
								"text": "删除线验证"
							},
							"type": "textRun"
						}
					],
					"style": {
						"list": {
							"indentLevel": 1,
							"number": 2,
							"type": "number"
						}
					}
				},
				"type": "paragraph"
			},
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {},
								"text": "有序标题3验证，"
							},
							"type": "textRun"
						},
						{
							"textRun": {
								"style": {
									"backColor": {
										"alpha": 1,
										"blue": 188,
										"green": 191,
										"red": 251
									},
									"textColor": {
										"alpha": 1,
										"blue": 49,
										"green": 57,
										"red": 216
									}
								},
								"text": "字体背景颜色验证"
							},
							"type": "textRun"
						}
					],
					"style": {
						"list": {
							"indentLevel": 1,
							"number": 3,
							"type": "number"
						}
					}
				},
				"type": "paragraph"
			},
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {},
								"text": "无序标题1验证，"
							},
							"type": "textRun"
						},
						{
							"textRun": {
								"style": {
									"bold": true
								},
								"text": "粗体"
							},
							"type": "textRun"
						}
					],
					"style": {
						"list": {
							"indentLevel": 1,
							"type": "bullet"
						}
					}
				},
				"type": "paragraph"
			},
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {},
								"text": "无序标题2验证，"
							},
							"type": "textRun"
						},
						{
							"textRun": {
								"style": {
									"strikeThrough": true
								},
								"text": "删除线"
							},
							"type": "textRun"
						}
					],
					"style": {
						"list": {
							"indentLevel": 1,
							"type": "bullet"
						}
					}
				},
				"type": "paragraph"
			},
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {},
								"text": "无序标题3验证，"
							},
							"type": "textRun"
						},
						{
							"textRun": {
								"style": {
									"backColor": {
										"alpha": 1,
										"blue": 188,
										"green": 191,
										"red": 251
									},
									"textColor": {
										"alpha": 1,
										"blue": 49,
										"green": 57,
										"red": 216
									}
								},
								"text": "字体背景颜色验证"
							},
							"type": "textRun"
						}
					],
					"style": {
						"list": {
							"indentLevel": 1,
							"type": "bullet"
						}
					}
				},
				"type": "paragraph"
			},
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {
									"link": {
										"url": "https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc"
									}
								},
								"text": "https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc"
							},
							"type": "textRun"
						}
					]
				},
				"type": "paragraph"
			},
			{
				"gallery": {
					"imageList": [
						{
							"fileToken": "boxbcofrHwpgexwxyvgasR2kgRh",
							"height": 372,
							"src": "https://internal-api-okr.feishu-boe.cn/stream/api/downloadFile/?file_token=boxbcofrHwpgexwxyvgasR2kgRh&ticket=eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJ0YXJnZXRfaWQiOiI3MDQxNDMwMzc3NjQyMDgyMzIzIiwidGFyZ2V0X3R5cGUiOjMsImFjdGlvbiI6MiwiZmlsZV90b2tlbiI6ImJveGJjb2ZySHdwZ2V4d3h5dmdhc1Iya2dSaCIsInVzZXJfaWQiOiI2OTY5ODU1NTAxNzQ0ODM0MDkyIiwidGVuYW50X2lkIjoiNjg3NzUwMjY4NzYwOTQwNjk5MCIsImV4cCI6MTY0MDE1NjEyMX0.PSs94Z6ljo4e7U5cFV8dYW-bNDUOWdKXRK8B-XKruGCtKWrhsFLNKbNygUkOgHzbiPg65aSAiCaWyhh5YeX0aw",
							"width": 458
						}
					]
				},
				"type": "gallery"
			},
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {},
								"text": "任务列表未勾选验证"
							},
							"type": "textRun"
						}
					],
					"style": {
						"list": {
							"indentLevel": 1,
							"type": "checkBox"
						}
					}
				},
				"type": "paragraph"
			},
			{
				"paragraph": {
					"elements": [
						{
							"textRun": {
								"style": {},
								"text": "任务列表已勾选验证"
							},
							"type": "textRun"
						}
					],
					"style": {
						"list": {
							"indentLevel": 1,
							"type": "checkedBox"
						}
					}
				},
				"type": "paragraph"
			}
		]
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
	"github.com/larksuite/oapi-sdk-go/v3/service/okr/v1"
)

// SDK 使用文档：https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/server-side-sdk/golang-sdk-guide/preparations
// 复制该 Demo 后, 需要将 "YOUR_APP_ID", "YOUR_APP_SECRET" 替换为自己应用的 APP_ID, APP_SECRET.
// 以下示例代码默认根据文档示例值填充，如果存在代码问题，请在 API 调试台填上相关必要参数后再复制代码使用
func main() {
	// 创建 Client
	client := lark.NewClient("YOUR_APP_ID", "YOUR_APP_SECRET")
	// 创建请求对象
	req := larkokr.NewUpdateProgressRecordReqBuilder().
		ProgressId(`7041857032248410131`).
		UserIdType(`open_id`).
		Body(larkokr.NewUpdateProgressRecordReqBodyBuilder().
			Content(larkokr.NewContentBlockBuilder().
				Blocks([]*larkokr.ContentBlockElement{
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`粗体更新`).
										Style(larkokr.NewContentTextStyleBuilder().
											Bold(true).
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`*`).
										Style(larkokr.NewContentTextStyleBuilder().
											Bold(true).
											Build()).
										Build()).
									Build(),
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`删除线更新`).
										Style(larkokr.NewContentTextStyleBuilder().
											StrikeThrough(true).
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`字体颜色更新`).
										Style(larkokr.NewContentTextStyleBuilder().
											TextColor(larkokr.NewContentColorBuilder().
												Red(216).
												Green(57).
												Blue(49).
												Alpha(1).
												Build()).
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`背景颜色验证`).
										Style(larkokr.NewContentTextStyleBuilder().
											BackColor(larkokr.NewContentColorBuilder().
												Red(251).
												Green(191).
												Blue(188).
												Alpha(1).
												Build()).
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`粗体+删除+字体颜色+背景颜色验证`).
										Style(larkokr.NewContentTextStyleBuilder().
											Bold(true).
											StrikeThrough(true).
											BackColor(larkokr.NewContentColorBuilder().
												Red(251).
												Green(191).
												Blue(188).
												Alpha(1).
												Build()).
											TextColor(larkokr.NewContentColorBuilder().
												Red(216).
												Green(57).
												Blue(49).
												Alpha(1).
												Build()).
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Style(larkokr.NewContentParagraphStyleBuilder().
								List(larkokr.NewContentListBuilder().
									Type(`number`).
									IndentLevel(1).
									Number(1).
									Build()).
								Build()).
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`有序标题1验证，`).
										Style(larkokr.NewContentTextStyleBuilder().
											Build()).
										Build()).
									Build(),
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`粗体验证`).
										Style(larkokr.NewContentTextStyleBuilder().
											Bold(true).
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Style(larkokr.NewContentParagraphStyleBuilder().
								List(larkokr.NewContentListBuilder().
									Type(`number`).
									IndentLevel(1).
									Number(2).
									Build()).
								Build()).
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`有序标题2验证，`).
										Style(larkokr.NewContentTextStyleBuilder().
											Build()).
										Build()).
									Build(),
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`删除线验证`).
										Style(larkokr.NewContentTextStyleBuilder().
											StrikeThrough(true).
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Style(larkokr.NewContentParagraphStyleBuilder().
								List(larkokr.NewContentListBuilder().
									Type(`number`).
									IndentLevel(1).
									Number(3).
									Build()).
								Build()).
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`有序标题3验证，`).
										Style(larkokr.NewContentTextStyleBuilder().
											Build()).
										Build()).
									Build(),
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`字体背景颜色验证`).
										Style(larkokr.NewContentTextStyleBuilder().
											BackColor(larkokr.NewContentColorBuilder().
												Red(251).
												Green(191).
												Blue(188).
												Alpha(1).
												Build()).
											TextColor(larkokr.NewContentColorBuilder().
												Red(216).
												Green(57).
												Blue(49).
												Alpha(1).
												Build()).
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Style(larkokr.NewContentParagraphStyleBuilder().
								List(larkokr.NewContentListBuilder().
									Type(`bullet`).
									IndentLevel(1).
									Build()).
								Build()).
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`无序标题1验证，`).
										Style(larkokr.NewContentTextStyleBuilder().
											Build()).
										Build()).
									Build(),
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`粗体`).
										Style(larkokr.NewContentTextStyleBuilder().
											Bold(true).
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Style(larkokr.NewContentParagraphStyleBuilder().
								List(larkokr.NewContentListBuilder().
									Type(`bullet`).
									IndentLevel(1).
									Build()).
								Build()).
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`无序标题2验证，`).
										Style(larkokr.NewContentTextStyleBuilder().
											Build()).
										Build()).
									Build(),
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`删除线`).
										Style(larkokr.NewContentTextStyleBuilder().
											StrikeThrough(true).
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Style(larkokr.NewContentParagraphStyleBuilder().
								List(larkokr.NewContentListBuilder().
									Type(`bullet`).
									IndentLevel(1).
									Build()).
								Build()).
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`无序标题3验证，`).
										Style(larkokr.NewContentTextStyleBuilder().
											Build()).
										Build()).
									Build(),
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`字体背景颜色验证`).
										Style(larkokr.NewContentTextStyleBuilder().
											BackColor(larkokr.NewContentColorBuilder().
												Red(251).
												Green(191).
												Blue(188).
												Alpha(1).
												Build()).
											TextColor(larkokr.NewContentColorBuilder().
												Red(216).
												Green(57).
												Blue(49).
												Alpha(1).
												Build()).
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc`).
										Style(larkokr.NewContentTextStyleBuilder().
											Link(larkokr.NewContentLinkBuilder().
												Url(`https://example/docx/doxcnO2Wkq0YPZQYLuJKyyOvLrh#doxcnSOui82swqk6c0o436Ak3nc`).
												Build()).
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`gallery`).
						Gallery(larkokr.NewContentGalleryBuilder().
							ImageList([]*larkokr.ContentImageItem{
								larkokr.NewContentImageItemBuilder().
									FileToken(`boxbcofrHwpgexwxyvgasR2kgRh`).
									Src(`https://internal-api-okr.feishu-boe.cn/stream/api/downloadFile/?file_token=boxbcofrHwpgexwxyvgasR2kgRh&ticket=eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJ0YXJnZXRfaWQiOiI3MDQxNDMwMzc3NjQyMDgyMzIzIiwidGFyZ2V0X3R5cGUiOjMsImFjdGlvbiI6MiwiZmlsZV90b2tlbiI6ImJveGJjb2ZySHdwZ2V4d3h5dmdhc1Iya2dSaCIsInVzZXJfaWQiOiI2OTY5ODU1NTAxNzQ0ODM0MDkyIiwidGVuYW50X2lkIjoiNjg3NzUwMjY4NzYwOTQwNjk5MCIsImV4cCI6MTY0MDE1NjEyMX0.PSs94Z6ljo4e7U5cFV8dYW-bNDUOWdKXRK8B-XKruGCtKWrhsFLNKbNygUkOgHzbiPg65aSAiCaWyhh5YeX0aw`).
									Width(458).
									Height(372).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Style(larkokr.NewContentParagraphStyleBuilder().
								List(larkokr.NewContentListBuilder().
									Type(`checkBox`).
									IndentLevel(1).
									Build()).
								Build()).
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`任务列表未勾选验证`).
										Style(larkokr.NewContentTextStyleBuilder().
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
					larkokr.NewContentBlockElementBuilder().
						Type(`paragraph`).
						Paragraph(larkokr.NewContentParagraphBuilder().
							Style(larkokr.NewContentParagraphStyleBuilder().
								List(larkokr.NewContentListBuilder().
									Type(`checkedBox`).
									IndentLevel(1).
									Build()).
								Build()).
							Elements([]*larkokr.ContentParagraphElement{
								larkokr.NewContentParagraphElementBuilder().
									Type(`textRun`).
									TextRun(larkokr.NewContentTextRunBuilder().
										Text(`任务列表已勾选验证`).
										Style(larkokr.NewContentTextStyleBuilder().
											Build()).
										Build()).
									Build(),
							}).
							Build()).
						Build(),
				}).
				Build()).
			Build()).
		Build()

	// 发起请求
	resp, err := client.Okr.V1.ProgressRecord.Update(context.Background(), req)

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

