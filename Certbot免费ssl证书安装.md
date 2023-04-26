---
title: "Certbot免费ssl证书安装"
date: 2023-03-29T21:04:34+08:00
draft: false
---

### 通过 SSH 连接到服务器
以具有 sudo 权限的用户身份通过 SSH 连接到运行 HTTP 网站的服务器。

### 安装
您需要安装 snapd 并确保按照任何说明启用经典快照支持。
sudo snap install core; sudo snap refresh core

删除 certbot-auto 和任何 Certbot OS 软件包

如果您使用操作系统包管理器（如、或）安装了任何Certbot软件包，则应在安装Certbot快照之前将其删除，以确保在运行命令时使用快照而不是从操作系统安装。 包管理器。执行此操作的确切命令取决于您的操作系统，但是 常见示例包括 、 或 。aptdnfyumcertbotsudo apt-get remove certbotsudo dnf remove certbotsudo yum remove certbot

### 安装certbot
在计算机上的命令行上运行此命令以安装 Certbot。

sudo snap install --classic certbot
准备 Certbot 命令
在计算机上的命令行上执行以下指令，以确保命令可以运行。certbot

sudo ln -s /snap/bin/certbot /usr/bin/certbot
选择您希望如何运行 Certbot
获取并安装证书...
运行此命令以获取证书，并让Certbot自动编辑您的nginx配置以提供它，只需一步即可打开HTTPS访问。

sudo certbot --nginx
或者，只是获得证书
如果您感觉更保守，并希望手动更改nginx配置，请运行此命令。

sudo certbot certonly --nginx
### 测试自动续订
您系统上的 Certbot 软件包附带一个 cron 作业或 systemd 计时器，它将在证书过期之前自动续订您的证书。除非您更改配置，否则无需再次运行 Certbot。您可以通过运行以下命令来测试证书的自动续订：

sudo certbot renew --dry-run
续订 certbot 的命令安装在以下位置之一：

/etc/crontab/
/etc/cron.*/*
systemctl list-timers
### 确认 Certbot 已正常工作
要确认您的网站设置正确，请访问浏览器并在 URL 栏中查找锁定图标。https://yourwebsite.com/
