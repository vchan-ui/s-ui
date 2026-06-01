## S-UI Pro Panel
基于 `SagerNet/Sing-Box` 构建的高性能 Web 管理面板

S-UI Pro Panel 为基于 [alireza0/s-ui](https://github.com/alireza0/s-ui) v1.4.1 的增强二次开发版本，在原有基础上进行了结构优化、界面升级与功能扩展。

Enhanced edition of [alireza0/s-ui](https://github.com/alireza0/s-ui) v1.4.1
> **免责声明：** 本项目仅用于学习与技术研究用途，请勿用于任何非法或违规用途。

| 功能                           |        是否支持        |
| ---------------------------- | :----------------: |
| 多协议                          | :heavy_check_mark: |
| 多语言                          | :heavy_check_mark: |
| 多客户端/入站                      | :heavy_check_mark: |
| 高级流量路由界面                     | :heavy_check_mark: |
| 客户端、流量与系统状态                  | :heavy_check_mark: |
| 订阅链接（link/json/clash + info） | :heavy_check_mark: |
| 深色/浅色主题                      | :heavy_check_mark: |
| API 接口                       | :heavy_check_mark: |
| 增强路由与可视化优化                   | :heavy_check_mark: |

| 平台      | 架构                                            | 状态    |
| ------- | --------------------------------------------- | ----- |
| Linux   | amd64, arm64, armv7, armv6, armv5, 386, s390x | 支持    |
| Windows | amd64, 386, arm64                             | 支持    |
| macOS   | amd64, arm64                                  | 实验性支持 |

⚙ 默认安装信息
面板端口：2095
面板路径：/app/
订阅端口：2096
订阅路径：/sub/
用户名/密码：admin

🚀 安装或升级到最新版本
Linux/macOS

bash <(curl -Ls https://raw.githubusercontent.com/vchan-ui/s-ui/main/install.sh)

📦 安装旧版本

如需安装指定版本，请在安装命令后追加版本号，例如：

v1.0.0
🛠 手动安装
Linux/macOS
下载 Release 包
解压到指定目录
安装 systemd 服务：
cp *.service /etc/systemd/system/
systemctl daemon-reload
启动服务：
systemctl enable s-ui --now
systemctl enable sing-box --now
Windows
下载 Windows ZIP 包
解压文件
管理员运行：
install-windows.bat

访问面板：
http://localhost:2095/app
❌ 卸载 S-UI Pro
sudo -i

systemctl disable s-ui --now

rm -f /etc/systemd/system/sing-box.service
systemctl daemon-reload

rm -rf /usr/local/s-ui
rm -f /usr/bin/s-ui

🐳 使用 Docker 安装
<details> <summary>点击查看详情</summary>
安装 Docker
curl -fsSL https://get.docker.com | sh
Docker Compose 部署
services:
  s-ui:
    image: ghcr.io/vchan-ui/s-ui
    container_name: s-ui
    hostname: "s-ui"
    network_mode: host
    volumes:
      - "./db:/app/db"
      - "./cert:/app/cert"
    restart: unless-stopped
docker compose up -d
  
Docker 直接运行
docker run -itd \
  --network host \
  -v $PWD/db:/app/db \
  -v $PWD/cert:/app/cert \
  --name s-ui \
  --restart=unless-stopped \
  ghcr.io/vchan-ui/s-ui
</details>

🧪 开发模式运行
<details> <summary>点击查看详情</summary>
git clone https://github.com/vchan-ui/s-ui
cd s-ui
./runSUI.sh
前端构建
rm -rf web/html/*
cp -R frontend/dist/ web/html/
后端构建
go build -o sui main.go
./sui
</details>

🌐 功能特性
多协议代理核心（基于 sing-box）
可视化入站 / 出站管理
用户流量与在线状态监控
订阅自动生成与管理
路由规则可视化配置
HTTPS 安全访问支持
🔧 环境变量
变量	类型	默认值
SUI_LOG_LEVEL	debug/info/warn/error	info
SUI_DEBUG	boolean	false
SUI_BIN_FOLDER	string	bin
SUI_DB_FOLDER	string	db
SINGBOX_API	string	-
🔐 SSL 证书
snap install core; snap refresh core
snap install --classic certbot
ln -s /snap/bin/certbot /usr/bin/certbot

certbot certonly --standalone \
-d yourdomain.com \
--non-interactive \
--agree-tos

🙏 致谢

本项目基于：

SagerNet / sing-box
原项目：alireza0/s-ui
📌 项目定位

S-UI Pro Panel 是一个面向多节点代理管理的轻量级控制面板，适用于个人与小型部署场景。
