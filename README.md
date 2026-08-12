# ruleset · 规则集订阅库

个人维护的 **sing-box / Clash (Mihomo)** 分流规则集订阅仓库，规则为个人网络分流配置，可直接通过订阅链接拉取使用，随维护实时更新。

## 规则集列表

| 规则集 | 格式 | 内容 | 用途 |
|--------|------|------|------|
| `proxy-domain` | yaml / json | Google 系域名等 | 🚀 走代理 |
| `direct-domain` | yaml / json | 国内服务、自有域名等 | DIRECT 直连 |
| `direct-ipcidr` | yaml / json | 直连 IP / CIDR | DIRECT 直连 |
| `emby-domain` | yaml / json | Emby 媒体服务器域名 | 🎥 Emby |

## 订阅链接

`<name>` 替换为 `proxy-domain` / `direct-domain` / `direct-ipcidr` / `emby-domain`：

| 方式 | 链接格式 |
|------|----------|
| jsDelivr CDN | `https://cdn.jsdelivr.net/gh/LAOFENG543/ruleset@main/rules/<name>.yaml` |
| GitHub Raw | `https://raw.githubusercontent.com/LAOFENG543/ruleset/main/rules/<name>.yaml` |

> 国内网络推荐优先使用 jsDelivr CDN。sing-box 用户使用同名 `.json` 文件（source 格式）。

## Clash / Mihomo 使用示例

### 1. 添加 rule-providers

```yaml
rule-providers:
  proxy-domain:
    type: http
    behavior: domain
    format: yaml
    path: ./ruleset/proxy-domain.yaml
    url: https://cdn.jsdelivr.net/gh/LAOFENG543/ruleset@main/rules/proxy-domain.yaml
    interval: 86400

  direct-domain:
    type: http
    behavior: domain
    format: yaml
    path: ./ruleset/direct-domain.yaml
    url: https://cdn.jsdelivr.net/gh/LAOFENG543/ruleset@main/rules/direct-domain.yaml
    interval: 86400

  direct-ipcidr:
    type: http
    behavior: ipcidr
    format: yaml
    path: ./ruleset/direct-ipcidr.yaml
    url: https://cdn.jsdelivr.net/gh/LAOFENG543/ruleset@main/rules/direct-ipcidr.yaml
    interval: 86400

  emby-domain:
    type: http
    behavior: domain
    format: yaml
    path: ./ruleset/emby-domain.yaml
    url: https://cdn.jsdelivr.net/gh/LAOFENG543/ruleset@main/rules/emby-domain.yaml
    interval: 86400
```

### 2. 在 rules 中引用（注意顺序，从上到下匹配）

```yaml
rules:
  - RULE-SET,direct-domain,DIRECT
  - RULE-SET,direct-ipcidr,DIRECT
  - RULE-SET,emby-domain,🎥 Emby
  - RULE-SET,proxy-domain,🚀 手动选择
  - MATCH,🚀 手动选择
```

## sing-box 使用示例（rule-set source 格式）

```json
{
  "route": {
    "rule_set": [
      {
        "tag": "emby",
        "type": "remote",
        "format": "source",
        "url": "https://cdn.jsdelivr.net/gh/LAOFENG543/ruleset@main/rules/emby-domain.json"
      }
    ],
    "rules": [
      { "rule_set": ["emby"], "action": "route", "outbound": "emby" }
    ]
  }
}
```

## 目录结构

```
ruleset/
├── rules/            # 规则集文件（yaml = Clash，json = sing-box source）
├── scripts/          # 规则生成/转换脚本（可选）
└── README.md
```

## 免责声明

本仓库仅供个人学习与网络调试使用，请遵守所在地区法律法规。
