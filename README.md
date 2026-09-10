# Sun-Panel for LazyCat

一个 NAS、服务器导航面板、简易 Docker 管理器、Homepage、浏览器首页。

主页：https://doc.sun-panel.top/zh_cn/

## 使用

要求懒猫微服 1.5.0 或更新版本，目标架构 amd64。默认账号 `admin@sun.cc`，默认密码 `12345678`，首次登录后请立即修改密码。保留手动登录，不注入文件选择器。

按 [当前部署文档](https://doc.sun-panel.top/zh_cn/usage/quick_deploy.html)，1.4.0 起 `/app/conf` 是配置、数据库、上传文件的合并目录，本包将其映射到 `/lzcapp/var/conf`。

保留 `/var/run/docker.sock`，通过 Compose 扩展挂载。目标微服需存在该 socket，并允许容器访问。它提供宿主 Docker 管理能力，请仅授权可信用户，不要随意改动微服管理的系统容器。

## 构建与发布

```sh
mkdir -p dist
lzc-cli project release -o dist/application.lpk
lzc-cli lpk info dist/application.lpk
```

仅发布到喵喵商店，官方商店关闭。使用 `docker.1ms.run/hslr/sun-panel` 镜像，自动更新会校验 amd64 摘要与上游相同。首次手动运行工作流填写 `1.8.1`，每日定时检查三段式稳定版本。

工作流引用组织级 `APPSTORE_URL`、`APPSTORE_TOKEN` 与可选的 `PRIVATE_STORE_GROUP_CODES`。发布文件名为 `community.lazycat.app.sun-panel-v<version>.lpk`，喵喵商店引用其 GitHub Release 下载地址和 SHA256。

图标由用户提供。本地构建和工作流检查不能替代微服上的 socket 权限、容器管理及界面实测。
