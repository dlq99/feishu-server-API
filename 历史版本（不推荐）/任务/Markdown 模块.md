# Markdown 模块
你可以使用标准markdown语法标签，快捷地构造富文本内容。

## 支持语法
<md-alert>
注意事项：<br>
- 目前只支持markdown语法的子集，支持的元素如下表：
</md-alert>



| 名称 | 语法                         | 效果        | 说明         | 可用范围        |
| --- | -------------------------   | ---------- | ----------- | --------- |
|@指定人|<at id=open_id></at><br><at id=user_id></at> | @用户名 | 注意：<br>自定义机器人仅支持使用open_id@人；应用机器人则支持权限范围内的3种@人方式 | 任务标题、任务备注、任务评论 |
|超链接|<a>https://open.example.com</a>|[https://open.example.com/](https://open.example.com/)|超链接必须包含schema才能生效，目前仅支持：https、http|任务标题、任务备注、任务评论|
|文字链接|\[测试网站\](https://open.example.com/)|[测试网站](https://open.example.com/)|超链接必须包含schema才能生效，目前仅支持：https、http|任务标题、任务备注、任务评论|

## 使用示例
目前可以使用Markdown模块的任务接口有创建任务、更新任务、创建评论、更新评论。每个接口使用Markdown模块的参数见各接口描述，这里以创建任务接口为例。
###  请求示例
创建任务接口使用Markdown模块生成富文本标题和备注的请求示例

```json 
 {
    "rich_summary": "这是user_id<at id=100001></at>[测试网站](https://open.example.com/)",
    "rich_description": "这是open_id<at id=ou_100001></at><a>https://open.example.com/xxxx</a>",
    "due": {
        "time": "1658962948",
        "timezone": "Asia/Shanghai",
        "is_all_day": false
    },
    "origin": {
        "platform_i18n_name": "{\"zh_cn\": \"IT 工作台\", \"en_us\": \"IT Workspace\"}",
        "href": {
            "url": "https://support.example.com/internal/foo-bar",
            "title": "反馈一个问题，需要协助排查"
        }
    },
    "repeat_rule": "FREQ=WEEKLY;INTERVAL=1;BYDAY=MO,TU,WE,TH,FR",
    "can_edit": true,
    "collaborator_ids": ["ou_100001", "ou_100002"],
    "follower_ids": ["ou_100003", "ou_100004"]
}
``` 
