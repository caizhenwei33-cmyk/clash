# Clash 配置仓库 / Clash Configuration Repository 🌐

[![Clash](https://img.shields.io/badge/Clash-Meta-blueviolet?style=flat-square)](https://github.com/MetaCubeX/Clash.Meta)
[![Clash Verge](https://img.shields.io/badge/Clash%20Verge-Rev-brightgreen?style=flat-square)](https://github.com/clash-verge-rev/clash-verge-rev)
[![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)

> 一份精心整理的 Clash / Clash Meta 配置教程和模板仓库，中英双语，开箱即用。
> A well-organized Clash / Clash Meta configuration tutorial and template repo, bilingual (Chinese + English), ready to use.

---

## 📖 目录 / Table of Contents

- [📖 目录 / Table of Contents](#-目录--table-of-contents)
- [🧠 什么是 Clash / What is Clash](#-什么是-clash--what-is-clash)
- [📥 安装方式 / Installation](#-安装方式--installation)
  - [Docker 部署 / Docker Deployment](#docker-部署--docker-deployment)
  - [原生安装 / Native Installation](#原生安装--native-installation)
- [⚙️ 配置文件详解 / Configuration Guide](#️-配置文件详解--configuration-guide)
  - [基础配置 / Basic Config](#基础配置--basic-config)
  - [代理节点 / Proxies](#代理节点--proxies)
  - [代理组 / Proxy Groups](#代理组--proxy-groups)
  - [规则 / Rules](#规则--rules)
- [🌐 代理协议说明 / Proxy Protocols](#-代理协议说明--proxy-protocols)
  - [VLESS](#vless)
  - [VMess](#vmess)
  - [Shadowsocks](#shadowsocks)
  - [Trojan](#trojan)
  - [Hysteria2](#hysteria2)
  - [TUIC](#tuic)
- [📊 Web 面板 / Web Dashboard](#-web-面板--web-dashboard)
  - [Yacd](#yacd)
  - [Razord](#razord)
- [📏 规则集与 DNS / Rule Sets & DNS](#-规则集与-dns--rule-sets--dns)
  - [规则集 / Rule Sets](#规则集--rule-sets)
  - [DNS 配置 / DNS Configuration](#dns-配置--dns-configuration)
- [🛠️ 常用命令与故障排查 / Commands & Troubleshooting](#️-常用命令与故障排查--commands--troubleshooting)
- [☕ 支持这个项目 / Support This Project](#-支持这个项目--support-this-project)

---

## 🧠 什么是 Clash / What is Clash

**中文**

[Clash](https://github.com/Dreamacro/clash) 是一个基于 Go 语言开发的跨平台代理客户端，支持多种代理协议（VMess、Shadowsocks、Trojan、VLESS、Hysteria2、TUIC 等）。它采用规则匹配引擎，能够根据你定义的规则智能分流流量——国内网站直连，国外网站走代理。

[Clash Meta](https://github.com/MetaCubeX/Clash.Meta) 是 Clash 的增强分支，增加了更多高级特性，如：Mux 多路复用、WireGuard 支持、新的核心、更好的性能等。[Clash Verge Rev](https://github.com/clash-verge-rev/clash-verge-rev) 是社区维护的 GUI 客户端，提供了图形化的配置管理界面。

**English**

[Clash](https://github.com/Dreamacro/clash) is a cross-platform proxy client written in Go, supporting multiple proxy protocols (VMess, Shadowsocks, Trojan, VLESS, Hysteria2, TUIC, etc.). It uses a rule-based matching engine to intelligently route traffic — domestic sites go direct, foreign sites go through proxies.

[Clash Meta](https://github.com/MetaCubeX/Clash.Meta) is an enhanced fork of Clash with advanced features like Mux multiplexing, WireGuard support, a new core, and better performance. [Clash Verge Rev](https://github.com/clash-verge-rev/clash-verge-rev) is the community-maintained GUI client with a user-friendly configuration interface.

**核心特性 / Core Features**

| 特性 / Feature | 说明 / Description |
|---|---|
| 🚀 多协议支持 | VMess, Shadowsocks, Trojan, VLESS, Hysteria2, TUIC |
| 🧠 规则引擎 / Rule Engine | DOMAIN, DOMAIN-SUFFIX, IP-CIDR, GEOIP, MATCH 等 |
| 🔄 自动切换 / Auto Switch | url-test / fallback / load-balance 策略组 |
| 📊 Web 面板 / Dashboard | Yacd, Razord 等可视化界面 |
| 🐳 Docker 支持 | 一键容器化部署 |

---

## 📥 安装方式 / Installation

### Docker 部署 / Docker Deployment

**中文**

使用 Docker 可以快速部署 Clash Meta，无需手动安装依赖。

**English**

Using Docker is the quickest way to deploy Clash Meta without manually installing dependencies.

```bash
# 创建配置目录 / Create config directory
mkdir -p /etc/clash

# 下载配置文件 / Download config
curl -o /etc/clash/config.yaml https://raw.githubusercontent.com/caizhenwei33-cmyk/clash/main/config.yaml

# 运行 Clash Meta 容器 / Run Clash Meta container
docker run -d \
  --name clash \
  --restart unless-stopped \
  -v /etc/clash:/root/.config/clash \
  -p 7890:7890 \
  -p 7891:7891 \
  -p 9090:9090 \
  ghcr.io/metacubex/clash-meta:latest
```

**验证 / Verify:**

```bash
# 检查容器状态 / Check container status
docker ps | grep clash

# 查看日志 / View logs
docker logs clash

# 测试代理 / Test proxy
curl -x http://127.0.0.1:7890 -I https://www.google.com
```

### 原生安装 / Native Installation

**中文**

**Linux (amd64 / arm64):**

**English**

```bash
# 下载最新版 Clash Meta / Download latest Clash Meta
# 访问 / Visit: https://github.com/MetaCubeX/Clash.Meta/releases

# 示例：Linux amd64 / Example: Linux amd64
wget https://github.com/MetaCubeX/Clash.Meta/releases/latest/download/clash.meta-linux-amd64.gz
gunzip clash.meta-linux-amd64.gz
chmod +x clash.meta-linux-amd64
sudo mv clash.meta-linux-amd64 /usr/local/bin/clash

# 创建配置目录 / Create config directory
mkdir -p ~/.config/clash

# 启动 / Start
clash -d ~/.config/clash
```

**macOS:**

```bash
# 使用 Homebrew / Using Homebrew
brew install clash-meta

# 启动 / Start
clash-meta -d ~/.config/clash
```

**Windows / GUI 客户端 / GUI Client:**

推荐使用 Clash Verge Rev——下载安装后导入配置文件即可。

We recommend Clash Verge Rev — download, install, and import your config file.

- 下载 / Download: https://github.com/clash-verge-rev/clash-verge-rev/releases

---

## ⚙️ 配置文件详解 / Configuration Guide

**中文**

Clash 使用 YAML 格式的配置文件。我们仓库中的 `config.yaml` 是一个完整的模板，以下是各部分详解。

**English**

Clash uses YAML-format configuration files. Our `config.yaml` is a complete template. Below is a detailed breakdown of each section.

### 基础配置 / Basic Config

```yaml
# HTTP 代理端口 / HTTP proxy port
port: 7890

# SOCKS5 代理端口 / SOCKS5 proxy port
socks-port: 7891

# 透明代理端口 / Transparent proxy port (Linux)
redir-port: 7892

# 允许局域网连接 / Allow LAN connections
allow-lan: true

# 运行模式 / Operation mode: Rule (规则), Global (全局), Direct (直连)
mode: Rule

# 日志级别 / Log level: info, warning, error, debug
log-level: info

# 外部控制 API / External controller API (用于 Web 面板 / for Web dashboard)
external-controller: 127.0.0.1:9090

# Web UI 目录 / Web UI directory
external-ui: ui
```

### 代理节点 / Proxies

**中文**

代理节点配置有两种方式：

1. **直接配置**：在 `proxies` 字段中逐个填写节点信息。
2. **订阅链接**：通过 `proxy-providers` 从远程订阅地址自动拉取。

**English**

There are two ways to configure proxies:

1. **Inline**: Define each proxy directly in the `proxies` field.
2. **Subscription**: Use `proxy-providers` to pull nodes from a remote subscription URL.

```yaml
# 方式一：直接配置 / Method 1: Inline config
proxies:
  - name: "🇭🇰 HK-01"
    type: vmess
    server: example.com
    port: 443
    uuid: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    alterId: 0
    cipher: auto
    tls: true
    network: ws
    ws-opts:
      path: /
      headers:
        Host: example.com

# 方式二：订阅链接 / Method 2: Subscription (推荐 / Recommended)
proxy-providers:
  Provider:
    type: http
    url: "https://example.com/sub?target=clash"  # 替换为你的订阅 / Replace with your sub URL
    interval: 86400          # 更新间隔（秒）/ Update interval (seconds)
    path: ./proxy_provider.yaml
    health-check:
      enable: true
      url: http://www.gstatic.com/generate_204
      interval: 300
```

### 代理组 / Proxy Groups

**中文**

代理组定义了流量的路由策略。Clash 支持多种策略类型：

| 策略类型 / Strategy | 说明 / Description |
|---|---|
| `select` | 手动选择 / Manual selection |
| `url-test` | 自动测速选最快 / Auto-select fastest by latency test |
| `fallback` | 按优先级依次尝试 / Try in priority order |
| `load-balance` | 负载均衡 / Load balance across proxies |

**English**

Proxy groups define the routing strategy for your traffic. Clash supports several strategy types.

```yaml
proxy-groups:
  # 自动选择（url-test：测速选最优）/ Auto (url-test: pick fastest)
  - name: 🚀 自动选择
    type: url-test
    proxies:
      - ♻️ 自动选择
      - DIRECT
    url: http://www.gstatic.com/generate_204
    interval: 300

  # 自动切换（fallback：按优先级）/ Auto fallback by priority
  - name: ♻️ 自动选择
    type: fallback
    use:
      - Provider
    url: http://www.gstatic.com/generate_204
    interval: 300

  # 手动选择国外流量 / Manual select for foreign traffic
  - name: 🌍 国外流量
    type: select
    proxies:
      - 🚀 自动选择
      - ♻️ 自动选择
      - DIRECT

  # 国内直连 / Direct for domestic traffic
  - name: 🎯 全球直连
    type: select
    proxies:
      - DIRECT
      - 🚀 自动选择

  # 兜底策略 / Catch-all fallback
  - name: 🐟 漏网之鱼
    type: select
    proxies:
      - 🚀 自动选择
      - ♻️ 自动选择
      - DIRECT
```

### 规则 / Rules

**中文**

规则从上到下依次匹配，匹配到后即停止。常用规则类型：

| 规则类型 / Rule Type | 示例 / Example |
|---|---|
| `DOMAIN-SUFFIX` | `DOMAIN-SUFFIX,google.com,Proxy` |
| `DOMAIN-KEYWORD` | `DOMAIN-KEYWORD,google,Proxy` |
| `DOMAIN` | `DOMAIN,google.com,Proxy` |
| `IP-CIDR` | `IP-CIDR,10.0.0.0/8,DIRECT` |
| `GEOIP` | `GEOIP,CN,DIRECT` |
| `DST-PORT` | `DST-PORT,443,Proxy` |
| `MATCH` | 兜底规则 / Default rule |

**English**

Rules are matched from top to bottom; the first matching rule takes effect.

```yaml
rules:
  # === 去广告 / Ad Blocking ===
  - DOMAIN-SUFFIX,adservice.google.com,🎯 全球直连
  - DOMAIN-SUFFIX,doubleclick.net,🎯 全球直连

  # === AI 服务走代理 / AI Services via Proxy ===
  - DOMAIN-SUFFIX,openai.com,🌍 国外流量
  - DOMAIN-SUFFIX,chatgpt.com,🌍 国外流量
  - DOMAIN-SUFFIX,claude.ai,🌍 国外流量
  - DOMAIN-SUFFIX,anthropic.com,🌍 国外流量

  # === 流媒体 / Streaming ===
  - DOMAIN-SUFFIX,youtube.com,🌍 国外流量
  - DOMAIN-SUFFIX,netflix.com,🌍 国外流量
  - DOMAIN-SUFFIX,spotify.com,🌍 国外流量

  # === 开发 / Development ===
  - DOMAIN-SUFFIX,github.com,🌍 国外流量
  - DOMAIN-SUFFIX,docker.com,🌍 国外流量
  - DOMAIN-SUFFIX,stackoverflow.com,🌍 国外流量

  # === 国内网站直连 / Domestic Direct ===
  - DOMAIN-SUFFIX,baidu.com,🎯 全球直连
  - DOMAIN-SUFFIX,qq.com,🎯 全球直连
  - DOMAIN-SUFFIX,bilibili.com,🎯 全球直连

  # === 内网地址直连 / LAN Direct ===
  - IP-CIDR,10.0.0.0/8,🎯 全球直连
  - IP-CIDR,172.16.0.0/12,🎯 全球直连
  - IP-CIDR,192.168.0.0/16,🎯 全球直连

  # === 兜底规则 / Catch-all Rule ===
  - MATCH,🐟 漏网之鱼
```

---

## 🌐 代理协议说明 / Proxy Protocols

**中文**

Clash 支持多种主流代理协议。以下是各协议的配置示例和说明。

**English**

Clash supports a wide range of proxy protocols. Below are configuration examples and explanations for each.

### VLESS

**中文**

VLESS 是 V2Ray 设计的轻量级传输协议，去掉了 VMess 的加密层，性能更好。通常与 XTLS/XRAY 配合使用。

**English**

VLESS is a lightweight transport protocol designed by V2Ray. It removes the encryption layer of VMess for better performance. Typically used with XTLS/XRAY.

```yaml
- name: "🇯🇵 JP-VLESS"
  type: vless
  server: jp.example.com
  port: 443
  uuid: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
  tls: true
  udp: true
  network: tcp
  flow: xtls-rprx-vision  # XTLS flow control
  servername: jp.example.com
```

### VMess

**中文**

VMess 是 V2Ray 的加密传输协议，也是 Clash 最广泛使用的协议之一。支持多种传输方式（TCP、WebSocket、gRPC 等）。

**English**

VMess is V2Ray's encrypted transport protocol and one of the most widely used protocols with Clash. It supports multiple transports (TCP, WebSocket, gRPC, etc.).

```yaml
- name: "🇭🇰 HK-VMess"
  type: vmess
  server: hk.example.com
  port: 443
  uuid: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
  alterId: 0
  cipher: auto
  tls: true
  udp: true
  network: ws
  ws-opts:
    path: /vmess
    headers:
      Host: hk.example.com
```

### Shadowsocks

**中文**

Shadowsocks 是一种轻量级代理协议，以简单高效著称。支持多种加密方式。

**English**

Shadowsocks is a lightweight proxy protocol known for its simplicity and efficiency. Supports multiple encryption methods.

```yaml
- name: "🇸🇬 SS-SG"
  type: ss
  server: sg.example.com
  port: 8388
  cipher: chacha20-ietf-poly1305
  password: your-password
  udp: true
```

### Trojan

**中文**

Trojan 协议通过伪装成 HTTPS 流量来绕过防火墙，配置简单且稳定。

**English**

Trojan camouflages as HTTPS traffic to bypass firewalls. It's simple to configure and stable.

```yaml
- name: "🇺🇸 US-Trojan"
  type: trojan
  server: us.example.com
  port: 443
  password: your-trojan-password
  udp: true
  sni: us.example.com
  skip-cert-verify: false
```

### Hysteria2

**中文**

Hysteria2 基于修改的 QUIC 协议，擅长在丢包率高或不稳定的网络环境下提供极速体验。使用 Brutal 拥塞控制算法。

**English**

Hysteria2 is based on a modified QUIC protocol. It excels in high packet-loss or unstable network environments, using the Brutal congestion control algorithm for maximum speed.

```yaml
- name: "🇯🇵 JP-Hy2"
  type: hysteria2
  server: jp.example.com
  port: 443
  password: your-hy2-password
  sni: jp.example.com
  skip-cert-verify: false
  up: 100  # Mbps - upload speed
  down: 200  # Mbps - download speed
```

### TUIC

**中文**

TUIC 是基于 QUIC 协议的轻量级代理，延迟低、性能好，适合游戏等对延迟敏感的场景。

**English**

TUIC is a lightweight proxy based on the QUIC protocol. It offers low latency and good performance, making it suitable for gaming and other latency-sensitive applications.

```yaml
- name: "🇰🇷 KR-TUIC"
  type: tuic
  server: kr.example.com
  port: 443
  token: your-tuic-token
  udp: true
  sni: kr.example.com
  skip-cert-verify: false
  congestion-controller: bbr  # or cubic
```

---

## 📊 Web 面板 / Web Dashboard

**中文**

Clash 提供了 RESTful API，第三方 Web 面板可以连接到 Clash 管理节点和策略。常用面板：

**English**

Clash provides a RESTful API. Third-party web dashboards can connect to Clash to manage proxies and policies. Popular dashboards:

### Yacd

[Yandex Clash Dashboard](https://github.com/haishanh/yacd) — 轻量美观的 Clash Web 面板。

A lightweight and beautiful Clash web dashboard.

```bash
# Docker 部署 Yacd / Deploy Yacd with Docker
docker run -d \
  --name yacd \
  --restart unless-stopped \
  -p 8080:80 \
  ghcr.io/haishanh/yacd:latest
```

访问 / Visit: `http://你的IP:8080`，输入 API 地址 `http://你的IP:9090` 即可连接。

Access `http://your-ip:8080` and enter the API URL `http://your-ip:9090` to connect.

### Razord

[Razord](https://github.com/Dreamacro/razord) — Clash 官方推荐的 Dashboard。

The officially recommended Clash dashboard.

```bash
# Docker 部署 Razord / Deploy Razord with Docker
docker run -d \
  --name razord \
  --restart unless-stopped \
  -p 8081:80 \
  dreamacro/razord:latest
```

访问 / Visit: `http://你的IP:8081`

---

## 📏 规则集与 DNS / Rule Sets & DNS

### 规则集 / Rule Sets

**中文**

Clash Meta 支持从远程加载规则集，方便管理和更新。常用规则集来源：

**English**

Clash Meta supports loading rule sets from remote URLs, making management and updates easier. Popular rule set sources:

```yaml
rule-providers:
  Reject:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/reject.txt"
    path: ./rules/reject.yaml
    interval: 86400

  Proxy:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/proxy.txt"
    path: ./rules/proxy.yaml
    interval: 86400

  Direct:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/direct.txt"
    path: ./rules/direct.yaml
    interval: 86400

  Apple:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/apple.txt"
    path: ./rules/apple.yaml
    interval: 86400

  Google:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/google.txt"
    path: ./rules/google.yaml
    interval: 86400

  GFW:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/gfw.txt"
    path: ./rules/gfw.yaml
    interval: 86400
```

然后在 rules 中引用 / Then reference them in rules:

```yaml
rules:
  - RULE-SET,Reject,🎯 全球直连
  - RULE-SET,Proxy,🌍 国外流量
  - RULE-SET,Direct,🎯 全球直连
  - RULE-SET,Apple,🎯 全球直连
  - RULE-SET,Google,🌍 国外流量
  - RULE-SET,GFW,🌍 国外流量
  - MATCH,🐟 漏网之鱼
```

### DNS 配置 / DNS Configuration

**中文**

合理配置 DNS 可以避免 DNS 污染，提高访问速度和安全性。

**English**

Proper DNS configuration prevents DNS poisoning and improves access speed and security.

```yaml
dns:
  enable: true
  listen: 0.0.0.0:53
  ipv6: true

  # 默认 DNS / Default DNS
  default-nameserver:
    - 114.114.114.114
    - 223.5.5.5
    - 1.1.1.1

  # 远程 DNS（用于代理域名）/ Remote DNS (for proxied domains)
  nameserver:
    - https://dns.alidns.com/dns-query
    - https://doh.pub/dns-query
    - tls://dns.google

  # 直连域名用国内 DNS / Direct domains use domestic DNS
  nameserver-policy:
    "geosite:cn": https://dns.alidns.com/dns-query
    "geosite:apple-cn": https://dns.alidns.com/dns-query

  # 缓存 / Cache
  cache:
    enable: true
    max-age: 3600
    max-count: 10000

  # 回退域名解析（防止 DNS 泄漏）/ Fallback (prevents DNS leaks)
  fallback:
    - tls://8.8.8.8
    - tls://1.1.1.1
    - https://dns.google/dns-query
  fallback-filter:
    geoip: true
    geoip-code: CN
    ipcidr:
      - 240.0.0.0/4
```

---

## 🛠️ 常用命令与故障排查 / Commands & Troubleshooting

**中文**

**常用命令 / Common Commands:**

**English**

```bash
# 检查配置文件是否正确 / Validate config file
clash -t -f config.yaml

# 以指定配置文件启动 / Start with specific config
clash -f config.yaml

# 指定工作目录启动 / Start with specific working directory
clash -d ~/.config/clash

# 测试代理是否可用（通过已运行的 Clash）/ Test if proxy is working
curl -x http://127.0.0.1:7890 -I https://www.google.com

# 查看 Clash API 状态 / Check Clash API status
curl http://127.0.0.1:9090/version

# 查看日志（实时）/ View logs (real-time)
docker logs -f clash
```

**常见问题 / Common Issues:**

| 问题 / Issue | 原因 / Cause | 解决方法 / Solution |
|---|---|---|
| ❌ 代理无法连接 | 配置文件中的节点信息错误 | 检查 `proxies` 或订阅链接是否正确 |
| ❌ 国内网站无法访问 | 规则配置错误 | 确保 `GEOIP,CN,DIRECT` 或国内域名规则在最前 |
| ❌ DNS 污染 / DNS Poisoning | 使用了有污染的 DNS | 配置 DNS over HTTPS/TLS，使用 `fallback-filter` |
| ❌ Web 面板无法连接 | `external-controller` 配置或端口被占用 | 检查 `external-controller` 地址和防火墙设置 |
| ❌ 订阅无法更新 | 订阅链接过期或网络不通 | 手动刷新或更换订阅链接 |
| ❌ 端口冲突 | 7890/7891 被其他程序占用 | 修改端口号或关闭冲突程序 |
| ⚠️ YAML 格式错误 | 缩进或语法问题 | 使用 `clash -t` 验证，或使用 YAML 校验工具 |

**Debug 模式 / Debug Mode:**

```yaml
# 在配置文件中设置 / In config file
log-level: debug
```

然后重启 Clash，查看详细的连接日志和规则匹配过程。

Then restart Clash to see detailed connection logs and rule matching process.

**重要提醒 / Important Notes:**

1. 配置文件中的 `proxies` 和 `proxy-providers` 需要替换为你自己的节点信息
2. 规则集仅供参考，请根据实际需要调整
3. 定期更新订阅链接以保持节点可用
4. 使用 Docker 部署时记得挂载配置目录

> 有任何问题或建议，欢迎提 Issue 或联系: **caizhenwei33@gmail.com**

---

## ☕ 支持这个项目 / Support This Project

如果你觉得这个教程对你有帮助，欢迎请我喝杯咖啡 ☕  
你的支持是我持续更新的最大动力！非常感谢！🙏

If you find this tutorial helpful, feel free to buy me a coffee ☕  
Your support is my biggest motivation to keep improving! Thank you so much! 🙏

**USDT (TRC20)**
```
TVbQerV1SF4MXB1JCcAzQxarewHwEPYTKm
```
