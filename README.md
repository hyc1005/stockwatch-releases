# StockWatch 下载

StockWatch 是 Windows 本地 A 股盯盘软件。本仓库只发布软件、SHA-256 校验文件和使用说明。

## 下载
- [最新版与更新说明](https://github.com/hyc1005/stockwatch-releases/releases/latest)
- [0.1.6 Windows x64 安装包](https://github.com/hyc1005/stockwatch-releases/releases/download/v0.1.6/StockWatch_0.1.6_x64-setup.exe)

公开下载无需 GitHub 登录。安装包适用于 Windows x64；Linux 云端机器可下载文件，运行桌面程序需 Windows 和桌面会话。升级前退出 StockWatch 和 AI 客户端的 StockWatch 连接。安装包未签名，目前通过手动安装升级。

## 云端机器获取最新版

读取公开 GitHub API 的 assets，选择名称符合 StockWatch_*_x64-setup.exe 的附件，使用 browser_download_url 下载。不要使用 Release 自动生成的 Source code 附件，它只包含本仓库说明。

~~~powershell
 = Invoke-RestMethod 'https://api.github.com/repos/hyc1005/stockwatch-releases/releases/latest'
 = .assets | Where-Object { .name -like 'StockWatch_*_x64-setup.exe' } | Select-Object -First 1
if (-not ) { throw '未找到 Windows 安装包' }
Invoke-WebRequest -Uri .browser_download_url -OutFile .name
~~~

固定版本也可直接下载：
~~~bash
curl -fL --retry 3 -o StockWatch_0.1.6_x64-setup.exe https://github.com/hyc1005/stockwatch-releases/releases/download/v0.1.6/StockWatch_0.1.6_x64-setup.exe
~~~

Release 的 SHA256SUMS.txt 用于核对安装包与 AI_TOOL_GUIDE.md。Windows 可用 Get-FileHash -Algorithm SHA256，Linux 可用 sha256sum -c SHA256SUMS.txt（需先下载清单列出的文件）。

## 0.1.6 AI 工具
支持本地 stdio MCP、20个工具、动态端口发现、独立授权和桌面确认的添加自选/创建观察/保存笔记。安装后在「设置 → AI工具接入」创建连接，详细步骤见 Release 附件 AI_TOOL_GUIDE.md。

外部 AI 客户端可能将返回数据发送到模型服务，请按需授权。当前只支持本地连接，云端机器下载到安装包不等于可以远程访问你电脑的 MCP。

基础自动测试及真实桌面升级/连接流程已通过。全新 Windows 安装与卸载，以及两个商业 AI 客户端的完整界面配置仍待验证。

问题反馈可在本仓库 Issues 提交，请勿上传凭据或个人数据。
