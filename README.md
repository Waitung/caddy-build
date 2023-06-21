# caddy build

caddy 自动构建
- https://github.com/caddyserver/caddy

```
xcaddy build $version --with $plugins
```

---

说明:  
脚本为[手动触发](../../actions/workflows/caddy-build.yml)，会提示输入**版本号**、**插件**，和选择**系统**

版本号：  
caddy 版本号，不能留空，格式参考 [xcaddy README](https://github.com/caddyserver/xcaddy#custom-builds)  
新增 `new` 并且作为默认值, **new** 为 releases 最新的 tag，类似 latest，但是包括 Pre-release 等

插件：  
caddy 插件，不能留空，默认值为:  
`caddy-dns/cloudflare mholt/caddy-webdav caddyserver/replace-response git001/caddyv2-upload`  
格式参考**默认值**，插件参考[官方下载页面](https://caddyserver.com/download), 只接受来自 github 的插件，默认会在前面补上 `github.com/`, 假设默认值，则实际执行以下命令构建:
```
xcaddy build $version \
  --with github.com/caddy-dns/cloudflare \
  --with github.com/mholt/caddy-webdav \
  --with github.com/caddyserver/replace-response \
  --with github.com/git001/caddyv2-upload
```

系统：  
目前只能选择 `linux` 或 `windows`, 默认为 `linux`  
参考 [golang 环境变量](https://go.dev/doc/install/source#environment)

---

自动上传到自己服务器，并使用 telegram 通知：  
需要手动触发(Run workflow)时，**上传** 手动选择`true`才会触发此作业  
另外还必须正确添加以下 [Repository secrets](../../settings/secrets/actions) :
  - **`UPLOAD_URL`** (上传的地址，例:`https://donamin.name/upload`)
  - **`UPLOAD_TOKEN`** (上传服务器的账号密码，例:`username:password`)
  - **`TG_TOKEN`** (telegram bot token ，例:`3269772492:mm8yjY8HzEA-WvFo6_Z9UfiknLLrjiu2iMj`)
  - **`TG_ID`** (telegram ID ，例:`2461963439`)
  - **`DL_URL`** (下载的地址，例:`https://donamin.name/download/caddy`)
