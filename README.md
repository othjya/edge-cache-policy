# edge-cache-policy

Personal edge asset routing policy.

This repository keeps a small supplemental rule list for selected high-volume asset and CDN endpoints. Broader upstream rules should remain outside this project.

## Remote Rule URL

```text
https://raw.githubusercontent.com/othjya/edge-cache-policy/main/rules/assets.list
```

## Mihomo Usage

Replace the local `自定义下载` provider with the remote one:

```yaml
rule-providers:
  自定义下载:
    <<: *Classical
    path: ./rules/EdgeAssets.list
    url: "https://raw.githubusercontent.com/othjya/edge-cache-policy/main/rules/assets.list"
```

Then route it to your download group before app/service rules:

```yaml
rules:
  - RULE-SET,自定义下载,下载流量
```

Recommended rule order:

```yaml
rules:
  - RULE-SET,No-ads-all_域,广告拦截
  - RULE-SET,自定义下载,下载流量
  - RULE-SET,Download_端/域,下载流量
  - RULE-SET,GameDownloadCN_域,🇨🇳 瓦洛兰大陆
  - RULE-SET,GameDownload_域,下载流量
```

## Maintenance Rules

- Prefer exact `DOMAIN` or scoped `DOMAIN-SUFFIX` entries.
- Do not add broad keyword rules such as `DOMAIN-KEYWORD,download` or `DOMAIN-KEYWORD,update`.
- Keep login, API, store, community, and account domains out of this list unless they are known to carry large downloads.
- If a domain is already covered by upstream `Download`, `GameDownload`, or `GameDownloadCN`, do not duplicate it here.

## Upstream Rules To Use With This Repo

```yaml
rule-providers:
  Download_端/域:
    <<: *Classical
    path: ./rules/Download.list
    url: "https://cdn.jsdelivr.net/gh/blackmatrix7/ios_rule_script@master/rule/Clash/Download/Download.list"

  GameDownload_域:
    <<: *Classical
    path: ./rules/GameDownload.list
    url: "https://cdn.jsdelivr.net/gh/blackmatrix7/ios_rule_script@master/rule/Clash/Game/GameDownload/GameDownload.list"

  GameDownloadCN_域:
    <<: *Classical
    path: ./rules/GameDownloadCN.list
    url: "https://cdn.jsdelivr.net/gh/blackmatrix7/ios_rule_script@master/rule/Clash/Game/GameDownloadCN/GameDownloadCN.list"
```

## Notes

Mihomo cannot classify traffic by transferred byte count in routing rules. This repo classifies selected high-volume traffic by domain and CDN hostname.
