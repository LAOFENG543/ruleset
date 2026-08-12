# ruleset · 规则集订阅库

个人维护的 **sing-box / Clash (Mihomo)** 分流规则集订阅仓库，规则为个人网络分流配置，可直接通过订阅链接拉取使用，随维护实时更新。

## 推荐：一条链接全搞定（all.yaml）

所有分流规则（含策略组）已合并为**一个文件**，配置里只需一个 rule-providers + 一条引用。

> 要求 **Mihomo / Clash.Meta 内核**（OpenClash 可切换内核为 Mihomo，Clash Party 默认为 Mihomo）。原版 Clash 内核不支持 classical 模式，请用下方"分文件方案"。

### 订阅链接

`https://cdn.jsdelivr.net/gh/LAOFENG543/ruleset@main/rules/all.yaml`

### 配置方法

`rule-providers:` 下加：

```yaml
rule-providers:
  all:
    type: http
    behavior: classical
    format: yaml
    path: ./ruleset/all.yaml
    url: https://cdn.jsdelivr.net/gh/LAOFENG543/ruleset@main/rules/all.yaml
    interval: 86400
```

`rules:` 段替换为：

```yaml
rules:
  - RULE-SET,all,🚀 手动选择
  - MATCH,🚀 手动选择
```

规则命中后按文件内行内策略组（DIRECT / 🎥 Emby / 🚀 手动选择）分流，无需在 rules 里逐条配置。

## 分文件方案（按策略组独立）

| 规则集 | 格式 | 内容 | 用途 |
|--------|------|------|------|
| `proxy-domain` | yaml / json | Google 系域名等 | 🚀 走代理 |
| `direct-domain` | yaml / json | 国内服务、自有域名等 | DIRECT 直连 |
| `direct-ipcidr` | yaml / json | 直连 IP / CIDR | DIRECT 直连 |
| `emby-domain` | yaml / json | Emby 媒体服务器域名 | 🎥 Emby |

订阅链接：`https://cdn.jsdelivr.net/gh/LAOFENG543/ruleset@main/rules/<name>.yaml`（sing-box 用户用同名 `.json`）。

### 分文件方案配置示例

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

## 维护说明

需要添加/修改规则时，直接更新对应 yaml 文件即可；客户端按 `interval: 86400`（24h）自动拉取，也可手动刷新。

## 免责声明

本仓库仅供个人学习与网络调试使用，请遵守所在地区法律法规。
