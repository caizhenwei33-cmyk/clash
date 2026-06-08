# Clash 配置仓库 🌐

个人 Clash / Clash Meta 配置备份，开箱即用。

## 文件说明

| 文件 | 说明 |
|------|------|
| `config.yaml` | 通用 Clash 配置文件模板 |
| `rules/` | 常用规则集（去广告、AI分流、流媒体等） |

## 快速使用

### Clash Verge（推荐）

1. 下载 [Clash Verge](https://github.com/clash-verge-rev/clash-verge-rev/releases)
2. 在订阅管理中添加订阅链接
3. 或者直接复制 `config.yaml` 内容粘贴到编辑器

### 直接使用

```bash
# 下载配置
curl -o config.yaml https://raw.githubusercontent.com/caizhenwei33-cmyk/clash/main/config.yaml

# 启动 Clash
clash -f config.yaml
```

## 注意

- 配置文件中的 `proxies` 和 `proxy-providers` 需要替换为你自己的节点信息
- 规则集仅供参考，按需调整

---

> 有问题请联系: **caizhenwei33@gmail.com**

## ☕ 支持 / Support

如果这个教程对你有帮助，欢迎请我喝杯咖啡：

**USDT (TRC20)**
```
TVbQerV1SF4MXB1JCcAzQxarewHwEPYTKm
```
