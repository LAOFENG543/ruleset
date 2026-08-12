# ruleset · 规则集订阅库

个人维护的 **sing-box / Clash (Mihomo)** 规则集订阅仓库，可直接通过订阅链接拉取使用，随维护实时更新。

## 目录结构

```
ruleset/
├── rules/            # 规则集文件
│   ├── *.srs         # sing-box rule-set 二进制格式
│   └── *.yaml        # Clash / Mihomo 规则集 (YAML)
├── scripts/          # 规则生成/转换脚本（可选）
└── README.md
```

## 订阅链接

所有规则集支持两种拉取方式（`<name>` 替换为对应文件名）：

| 方式 | 链接格式 |
|------|----------|
| GitHub Raw | `https://raw.githubusercontent.com/LAOFENG543/ruleset/main/rules/<name>` |
| jsDelivr CDN | `https://cdn.jsdelivr.net/gh/LAOFENG543/ruleset@main/rules/<name>` |

> 国内网络推荐优先使用 jsDelivr CDN 加速。

## 使用示例

### sing-box（rule-set 二进制 .srs）

```json
{
  "route": {
    "rule_set": [
      {
        "tag": "ads",
        "type": "remote",
        "format": "binary",
        "url": "https://cdn.jsdelivr.net/gh/LAOFENG543/ruleset@main/rules/ads.srs"
      }
    ]
  }
}
```

### Clash / Mihomo（YAML rule-set）

```yaml
rule-providers:
  ads:
    type: http
    behavior: domain
    format: yaml
    path: ./ruleset/ads.yaml
    url: https://cdn.jsdelivr.net/gh/LAOFENG543/ruleset@main/rules/ads.yaml
    interval: 86400
```

## 规则集列表

| 文件 | 格式 | 说明 |
|------|------|------|
| 维护中... | - | 规则集将陆续添加 |

## 免责声明

本仓库仅供个人学习与网络调试使用，请遵守所在地区法律法规。
