# StockWatch 下载

本仓库只分发软件、校验文件和使用说明，不包含应用源代码。

| 平台 | 版本 | 下载 |
| --- | --- | --- |
| Ubuntu 22.04/24.04 x64 无界面服务 | 0.1.7 | [Linux包](https://github.com/hyc1005/stockwatch-releases/releases/download/v0.1.7/StockWatch_0.1.7_linux_x64.tar.gz) |
| Windows x64 桌面版 | 0.1.6 | [Windows安装包](https://github.com/hyc1005/stockwatch-releases/releases/download/v0.1.6/StockWatch_0.1.6_x64-setup.exe) |

[最新Release](https://github.com/hyc1005/stockwatch-releases/releases/latest)提供对应平台的更新说明。公开附件无需登录GitHub；自动生成的Source code附件只包含本仓库下载说明。

## Linux与Hermes Agent

Linux包内包含stockwatchd后台服务、stdio MCP连接程序、授权CLI、systemd用户服务、安装脚本和Hermes接入说明。StockWatch运行无需桌面、Node.js或Rust开发环境。Hermes与服务应运行在同一虚拟机、同一普通用户下。

下载Linux包及同一Release的SHA256SUMS.txt，先校验再解压，运行包内install.sh。然后创建连接，将返回配置的command与args放入Hermes config.yaml的mcp_servers.stockwatch条目，执行hermes mcp test stockwatch。具体命令与权限说明见包内LINUX_HERMES_GUIDE.md。

首版最多16个读取工具，不开放业务写入或公网MCP。返回的数据可能由AI客户端发送至模型服务，请按需授权。

## 云端获取最新版Linux包

公开接口：https://api.github.com/repos/hyc1005/stockwatch-releases/releases/latest

选择assets中以_linux_x64.tar.gz结尾的附件，使用browser_download_url下载。Windows当前稳定包仍从上表的0.1.6下载；不要假定每个平台都有相同的最新版本。

固定Linux版本下载：
~~~bash
curl -fL --retry 3 -O https://github.com/hyc1005/stockwatch-releases/releases/download/v0.1.7/StockWatch_0.1.7_linux_x64.tar.gz
curl -fL --retry 3 -O https://github.com/hyc1005/stockwatch-releases/releases/download/v0.1.7/SHA256SUMS.txt
sha256sum --ignore-missing -c SHA256SUMS.txt
tar -xzf StockWatch_0.1.7_linux_x64.tar.gz
sh StockWatch_0.1.7_linux_x64/install.sh
~~~

Windows升级前退出软件和MCP连接。问题可在本仓库Issues反馈，请勿上传连接凭据或个人数据。
