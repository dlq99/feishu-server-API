# 获取 user_access_token

OAuth 令牌接口，可用于获取 <code>user_access_token</code> 以及 <code>refresh_token</code>。<code>user_access_token</code> 为用户访问凭证，使用该凭证可以以用户身份调用 OpenAPI。<code>refresh_token</code> 为刷新凭证，可以用来获取新的 <code>user_access_token</code>。


- 获取 `user_access_token` 前需要先获取授权码，详见获取授权码。请注意授权码的有效期为 5 分钟，且只能被使用一次。
- 获取到的 `user_access_token` 存在有效期，如何刷新 <code>user_access_token</code> 详见刷新 user_access_token。
- 如果你需要获取用户信息，详见获取用户信息。

<md-alert type="tip">
    本接口实现遵循 [RFC 6749 - The OAuth 2.0 Authorization Framework](https://datatracker.ietf.org/doc/html/rfc6749) ，你可以使用[标准的 OAuth 客户端库](https://oauth.net/code/)进行接入（**推荐**）
</md-alert>


## 请求

| 基本 |  |
| --- | --- |
| https://open.feishu.cn/open-apis/authen/v2/oauth/token |
| POST |
| 1000 次/分钟、50 次/秒 |
|  |
| 无 |
| `refresh_token` 以及 `refresh_token_expires_in` 字段仅在具备以下权限时返回：<br><br>offline_access |



### 请求头

| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| Content-Type | string | 是 | 请求体类型。<br><br>固定值：`application/json; charset=utf-8` |



### 请求体

| 名称 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |



### 请求体示例
```json
{
    "grant_type": "authorization_code",
    "client_id": "cli_a5ca35a685b0x26e",
    "client_secret": "baBqE5um9LbFGDy3X7LcfxQX1sqpXlwy",
    "code": "a61hb967bd094dge949h79bbexd16dfe",
    "redirect_uri": "https://example.com/api/oauth/callback",
    "code_verifier": "TxYmzM4PHLBlqm5NtnCmwxMH8mFlRWl_ipie3O0aVzo"
}
```
## 响应
响应体类型为 `application/json; charset=utf-8`。

### 响应体
<md-alert type="tip">**响应体中的 `access_token` 和 `refresh_token` 长度较长**，一般在 1~2KB 之间，且可能由于 `scope` 数量的变多或后续变更导致长度进一步增加，建议预留 4KB 的存储容量</md-alert>


| 名称 | 类型 | 描述 |
| --- | --- | --- |



### 响应体示例

成功响应示例：

```json
{
    "code": 0,
    "access_token": "eyJhbGciOiJFUzI1NiIs**********X6wrZHYKDxJkWwhdkrYg",
    "expires_in": 7200, // 非固定值，请务必根据响应体中返回的实际值来确定 access_token 的有效期
    "refresh_token": "eyJhbGciOiJFUzI1NiIs**********XXOYOZz1mfgIYHwM8ZJA",
    "refresh_token_expires_in": 604800, // 非固定值，请务必根据响应体中返回的实际值来确定 refresh_token 的有效期
    "scope": "auth:user.id:read offline_access task:task:read user_profile",
    "token_type": "Bearer"
}
```

失败响应示例：
```json
{
    "code": 20050,
    "error": "server_error",
    "error_description": "An unexpected server error occurred. Please retry your request."
}
```

### 错误码
| HTTP 状态码 | 错误码 | 描述 | 排查建议 |
| --- | --- | --- | --- |
| 400 | 20001 | The request is missing a required parameter. | 必要参数缺失，请检查请求时传入的参数是否有误 |
| 400 | 20002 | The client secret is invalid. | 应用认证失败，请检查提供的 `client_id` 与 `client_secret` 是否正确 |
| 400 | 20003 | The authorization code is not found. Please note that an authorization code can only be used once. | 无效的授权码，请检查授权码是否有效，注意授权码仅能使用一次 |
| 400 | 20004 | The authorization code has expired. | 授权码已经过期，请在授权码生成后的 5 分钟内使用 |
| 400 | 20008 | The user does not exist. | 用户不存在，请检查发起授权的用户的当前状态 |
| 400 | 20009 | The specified app is not installed. | 租户未安装应用，请检查应用状态 |
| 400 | 20010 | The user does not have permission to use this app. | 用户无应用使用权限，请检查发起授权的用户是否仍具有应用使用权限 |
| 400 | 20024 | The provided authorization code or refresh token does not match the provided client ID. | 提供的授权码与 `client_id` 不匹配，请勿混用不同应用的凭证 |
| 400 | 20036 | The specified grant_type is not supported. | 无效的 `grant_type`，请检查请求体中 `grant_type` 字段的取值 |
| 400 | 20048 | The specified app does not exist. | 应用不存在，请检查应用状态 |
| 400 | 20049 | PKCE code challenge failed. | PKCE 校验失败，请检查请求体中 `code_verifier` 字段是否存在且有效 |
| 500 | 20050 | An unexpected server error occurred. Please retry your request. | 内部服务错误，请稍后重试，如果持续报错请联系[技术支持](https://applink.feishu.cn/TLJpeNdW) |
| 400 | 20063 | The request is malformed. Please check your request. | 请求体中缺少必要字段，请根据具体的错误信息补齐字段 |
| 400 | 20065 | The authorization code has been used. Please note that an authorization code can only be used once. | 授权码已被使用，授权码仅能使用一次，请检查是否有被重复使用 |
| 400 | 20066 | The user status is invalid. | 用户状态非法，请检查发起授权的用户的当前状态 |
| 400 | 20067 | The provided scope list contains duplicate scopes. Please ensure all scopes are unique. | 无效的 `scope` 列表，其中存在重复项，请确保传入的 `scope` 列表中没有重复项 |
| 400 | 20068 | The provided scope list contains scopes that are not permitted. Please ensure all scopes are allowed. | 无效的 `scope` 列表，其中存在用户未授权的权限。当前接口 `scope` 参数传入的权限必须是获取授权码时 `scope` 参数值的子集。<br> <br>例如，在获取授权码时，用户授权了权限 A、B，则当前接口 `scope` 可传入的值只有权限 A、B，若传入权限 C 则会返回当前错误码。 |
| 400 | 20069 | The specified app is not enabled. | 应用未启用，请检查应用状态 |
| 400 | 20070 | Multiple authentication methods were provided. Please only use one to proceed. | 请求使用了 `Basic Authentication`，同时也在请求体中传递了 `client_secret`，请仅使用一种认证方式 |
| 400 | 20071 | The provided redirect URI does not match the one used during authorization. | 无效的 `redirect_uri`，请确保 `redirect_uri` 与获取授权码时传入的 `redirect_uri` 保持一致 |
| 503 | 20072 | The server is temporarily unavailable. Please retry your request. | 服务暂不可用，请稍后重试 |



## 代码示例
<md-alert type="warn">此处提供的代码示例**仅供参考**，请勿直接在生产环境使用
</md-alert>


### Golang

运行下面示例程序的步骤：
1. 点击下方代码块右上角复制按钮，将代码复制到本地文件中，保存为 `main.go`；
2. 参照注释部分，完成配置；
3. 在 `main.go` 所在目录下新建 `.env` 文件，内容如下：
    ```bash
    APP_ID=cli_xxxxxx # 仅为示例值，请使用你的应用的 App ID，获取方式：开发者后台 -> 基础信息 -> 凭证与基础信息 -> 应用凭证 -> App ID
	APP_SECRET=xxxxxx # 仅为示例值，请使用你的应用的 App Secret，获取方式：开发者后台 -> 基础信息 -> 凭证与基础信息 -> 应用凭证 -> App Secret
    ```
4. 在 `main.go` 所在目录执行以下命令：
	```bash
    go mod init oauth-test
	go get github.com/gin-gonic/gin
	go get github.com/gin-contrib/sessions
	go get github.com/gin-contrib/sessions/cookie
	go get github.com/joho/godotenv
	go get golang.org/x/oauth2
	go run main.go
    ```
5. 浏览器打开 [http://localhost:8080](http://localhost:8080) ，按照页面提示完成授权流程；

```javascript
package main

import (
    "context"
    "encoding/json"
    "fmt"
    "log"
    "math/rand"
    "net/http"
    "os"

    "github.com/gin-contrib/sessions"
    "github.com/gin-contrib/sessions/cookie"
    "github.com/gin-gonic/gin"
    _ "github.com/joho/godotenv/autoload"
    "golang.org/x/oauth2"
)

var oauthEndpoint = oauth2.Endpoint{
    AuthURL:  "https://accounts.feishu.cn/open-apis/authen/v1/authorize",
    TokenURL: "https://open.feishu.cn/open-apis/authen/v2/oauth/token",
}

var oauthConfig = &oauth2.Config{
    ClientID:     os.Getenv("APP_ID"),
    ClientSecret: os.Getenv("APP_SECRET"),
    RedirectURL:  "http://localhost:8080/callback", // 请先添加该重定向 URL，配置路径：开发者后台 -> 开发配置 -> 安全设置 -> 重定向 URL -> 添加
    Endpoint:     oauthEndpoint,
    Scopes:       []string{"offline_access"}, // 如果你不需要 refresh_token，请注释掉该行，否则你需要先申请 offline_access 权限方可使用，配置路径：开发者后台 -> 开发配置 -> 权限管理      
}

func main() {
    r := gin.Default()

    // 使用 Cookie 存储 session
    store := cookie.NewStore([]byte("secret")) // 此处仅为示例，务必不要硬编码密钥
    r.Use(sessions.Sessions("mysession", store))

    r.GET("/", indexController)
    r.GET("/login", loginController)
    r.GET("/callback", oauthCallbackController)

    fmt.Println("Server running on http://localhost:8080")
    log.Fatal(r.Run(":8080"))
}

func indexController(c *gin.Context) {
    c.Header("Content-Type", "text/html; charset=utf-8")
    var username string
    session := sessions.Default(c)
    if session.Get("user") != nil {
       username = session.Get("user").(string)
    }
    html := fmt.Sprintf(`<html><head><style>body{font-family:Arial,sans-serif;background:#f4f4f4;margin:0;display:flex;justify-content:center;align-items:center;height:100vh}.container{text-align:center;background:#fff;padding:30px;border-radius:10px;box-shadow:0 0 10px rgba(0,0,0,0.1)}a{padding:10px 20px;font-size:16px;color:#fff;background:#007bff;border-radius:5px;text-decoration:none;transition:0.3s}a:hover{background:#0056b3}}</style></head><body><div class="container"><h2>欢迎%s！</h2><a href="/login">使用飞书登录</a></div></body></html>`, username)
    c.String(http.StatusOK, html)
}

func loginController(c *gin.Context) {
    session := sessions.Default(c)

    // 生成随机 state 字符串，你也可以用其他有意义的信息来构建 state
    state := fmt.Sprintf("%d", rand.Int())
    // 将 state 存入 session 中
    session.Set("state", state)
    // 生成 PKCE 需要的 code verifier
    verifier := oauth2.GenerateVerifier()
    // 将 code verifier 存入 session 中
    session.Set("code_verifier", verifier)
    session.Save()

    url := oauthConfig.AuthCodeURL(state, oauth2.S256ChallengeOption(verifier))
    // 用户点击登录时，重定向到授权页面
    c.Redirect(http.StatusTemporaryRedirect, url)
}

func oauthCallbackController(c *gin.Context) {
    session := sessions.Default(c)
    ctx := context.Background()

    // 从 session 中获取 state
    expectedState := session.Get("state")
    state := c.Query("state")

    // 如果 state 不匹配，说明是 CSRF 攻击，拒绝处理
    if state != expectedState {
       log.Printf("invalid oauth state, expected '%s', got '%s'\n", expectedState, state)
       c.Redirect(http.StatusTemporaryRedirect, "/")
       return
    }

    code := c.Query("code")
    // 如果 code 为空，说明用户拒绝了授权
    if code == "" {
       log.Printf("error: %s", c.Query("error"))
       c.Redirect(http.StatusTemporaryRedirect, "/")
       return
    }
    codeVerifier, _ := session.Get("code_verifier").(string)
    // 使用获取到的 code 获取 token
    token, err := oauthConfig.Exchange(ctx, code, oauth2.VerifierOption(codeVerifier))
    if err != nil {
       log.Printf("oauthConfig.Exchange() failed with '%s'\n", err)
       c.Redirect(http.StatusTemporaryRedirect, "/")
       return
    }

    client := oauthConfig.Client(ctx, token)

    req, err := http.NewRequest("GET", "https://open.feishu.cn/open-apis/authen/v1/user_info", nil)
    if err != nil {
       log.Fatal(err)
    }
    req.Header.Set("Authorization", "Bearer "+token.AccessToken)

    // 使用 token 发起请求，获取用户信息
    resp, err := client.Do(req)
    if err != nil {
       log.Printf("client.Get() failed with '%s'\n", err)
       c.Redirect(http.StatusTemporaryRedirect, "/")
       return
    }
    defer resp.Body.Close()

    var user struct {
       Data struct {
          Name string `json:"name"`
       } `json:"data"`
    }
    if err := json.NewDecoder(resp.Body).Decode(&user); err != nil {
       log.Printf("json.NewDecoder() failed with '%s'\n", err)
       c.Redirect(http.StatusTemporaryRedirect, "/")
       return
    }
    // 后续可以用获取到的用户信息构建登录态，此处仅为示例，请勿直接使用
    session.Set("user", user.Data.Name)
    session.Save()

    c.Header("Content-Type", "text/html; charset=utf-8")
    html := fmt.Sprintf(`<html><head><style>body{font-family:Arial,sans-serif;background:#f4f4f4;margin:0;display:flex;justify-content:center;align-items:center;height:100vh}.container{text-align:center;background:#fff;padding:30px;border-radius:10px;box-shadow:0 0 10px rgba(0,0,0,0.1)}a{padding:10px 20px;font-size:16px;color:#fff;background:#007bff;border-radius:5px;text-decoration:none;transition:0.3s}a:hover{background:#0056b3}}</style></head><body><div class="container"><h2>你好，%s！</h2><p>你已成功完成授权登录流程。</p><a href="/">返回主页</a></div></body></html>`, user.Data.Name)
    c.String(http.StatusOK, html)
}
```