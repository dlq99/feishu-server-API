# 获取我的空间（root folder）元数据

该接口用于获取用户“我的空间”（root folder）的元数据，包括文件夹的 token、ID 和文件夹所有者的 ID。

## 请求
| 基本 |  |
| --- | --- |
| https://open.feishu.cn/open-apis/drive/explorer/v2/root_folder/meta |
| GET |
|  |
| 查看、评论、编辑和管理云空间中所有文件<br>查看云空间中文件元数据 |



<md-alert type="tip">
了解更多权限相关信息，参考云文档常见问题。
</md-alert>

### 请求头
| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| Authorization | string | 是 | 应用调用 API 时，需要通过访问凭证（access_token）进行身份鉴权，参考选择并获取访问凭证。<br><br>值格式："Bearer `access_token`"<br> <br>可选值如下：<br>- `tenant_access_token`：<br> <br> 以应用身份调用 API，可读写的数据范围由应用自身的数据权限范围决定。参考自建应用获取 tenant_access_token或商店应用获取 tenant_access_token。示例值："Bearer t-g1044qeGEDXTB6NDJOGV4JQCYDGHRBARFTGT1234"<br> <br>- `user_access_token`：<br> <br> 以用户身份调用 API，可读写的数据范围由用户的的数据权限范围决定。参考获取 user_access_token。示例值："Bearer u-cjz1eKCEx289x1TXEiQJqAh5171B4gDHPq00l0GE1234" |




### cURL示例
```bash
curl --location 'https://open.feishu.cn/open-apis/drive/explorer/v2/root_folder/meta' \
--header 'Authorization: Bearer t-e13d5ec1954e82e458f3ce04491c54ea8c9abcef'
```

## 响应
  
### 响应体


<md-dt-table>
  <md-dt-thead>
      <md-dt-tr>
      <md-dt-th style="width: 15%;">名称</md-dt-th>
      <md-dt-th style="width: 13%;">类型</md-dt-th>
      <md-dt-th style="width: 52%;">描述</md-dt-th>
      </md-dt-tr>
  </md-dt-thead>
  <md-dt-tbody>

<md-dt-tr level="0">
	<md-dt-td>
	token
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	文件夹的 token
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="0">
	<md-dt-td>
	id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	文件夹的 ID
	</md-dt-td>
</md-dt-tr>


<md-dt-tr level="0">
	<md-dt-td>
	user_id
	</md-dt-td>
	<md-dt-td>
	string
	</md-dt-td>
	<md-dt-td>
	文件夹所有者的 ID
	</md-dt-td>
</md-dt-tr>
  </md-dt-tbody>
</md-dt-table>


    
### 响应体示例
```json
{
  "code": 0,
  "msg": "Success",
  "data": {
    "token": "nodbcbHUdOsS613xVzTzFEabcef",
    "id": "7110173013420512356",
    "user_id": "7103496998321312356"
	}
}
```
  
### 错误码

以下为本接口相关错误码。了解其它通用错误码，参考通用错误码。

| 错误码 | 错误信息 | 排查建议 |
| --- | --- | --- |
| 91201 | FAILED | 处理失败。请稍后重试。 |
| 91204 | FORBIDDEN | 当前应用或用户没有权限。参考本文档“请求”部分的权限要求为应用或用户开启对应权限。了解更多，参考云空间常见问题。 |


