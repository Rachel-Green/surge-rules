# 简介

本项目生成适用于 [**Surge**](https://nssurge.com) 的规则集（DOMAIN-SET）。使用 GitHub Actions 北京时间每天早上 6:30 自动构建，保证规则最新。

## 说明

本项目的规则集（DOMAIN-SET）主要来源于项目 [@Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat) 和 [@v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)；[`Apple`](https://github.com/Loyalsoldier/surge-rules/blob/release/apple.txt) 和 [`Google`](https://github.com/Loyalsoldier/surge-rules/blob/release/google.txt) 列表里的部分域名来源于项目 [@felixonmars/dnsmasq-china-list](https://github.com/felixonmars/dnsmasq-china-list)；中国大陆 IPv4 地址数据使用 [@17mon/china_ip_list](https://github.com/17mon/china_ip_list)。

本项目的规则集（DOMAIN-SET）只适用于 Surge for Mac **Version 3.5.1** 及更新的版本。

## 规则文件地址及使用方式

### 在线地址（URL）

> 如果无法访问域名 `raw.githubusercontent.com`，可以使用第二个地址（`cdn.jsdelivr.net`），但是内容更新会有 12 小时的延迟。

- **直连域名列表 direct.txt**：
  - [https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/direct.txt](https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/direct.txt)
  - [https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/direct.txt](https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/direct.txt)
- **代理域名列表 proxy.txt**：
  - [https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/proxy.txt](https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/proxy.txt)
  - [https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/proxy.txt](https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/proxy.txt)
- **广告域名列表 reject.txt**：
  - [https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/reject.txt](https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/reject.txt)
  - [https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/reject.txt](https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/reject.txt)
- **Apple 域名列表 apple.txt**：
  - [https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/apple.txt](https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/apple.txt)
  - [https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/apple.txt](https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/apple.txt)
- **iCloud 域名列表 icloud.txt**：
  - [https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/icloud.txt](https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/icloud.txt)
  - [https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/icloud.txt](https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/icloud.txt)
- **Google 域名列表 google.txt**：
  - [https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/google.txt](https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/google.txt)
  - [https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/google.txt](https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/google.txt)
- **中国大陆 IPv4 地址列表 cncidr.txt**：
  - [https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/cncidr.txt](https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/cncidr.txt)
  - [https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/cncidr.txt](https://cdn.jsdelivr.net/gh/Loyalsoldier/surge-rules@release/cncidr.txt)

### 使用方式

关于 Surge 的详细使用方法，见[官方手册](https://manual.nssurge.com)。要想使用本项目的规则集，只需要在 Surge 配置文件中添加如下规则。

- 如果希望使用 DNS 来解析未命中域名类型规则的域名，而不是直接走代理，请删除 `cncidr` 行尾的 `,no-resolve`。
- 以下配置中，除了 `DIRECT` 和 `REJECT` 是默认存在于 Surge 中的 policy（路由策略/流量处理策略），其余均为自定义 policy，对应配置文件中 `[Proxy]` 或 `[Proxy Group]` 中的代理名称。如你直接使用下面的 `[Rule]` 规则，则需要在 `[Proxy]` 或 `[Proxy Group]` 中手动配置一个名为 `PROXY` 的 policy。
- 如你希望 Apple、iCloud 和 Google 列表中的域名使用代理，则把 policy 由 `DIRECT` 改为 `PROXY`，以此类推，举一反三。

```
[Rule]
PROCESS-NAME,v2ray,DIRECT
PROCESS-NAME,clash,DIRECT
PROCESS-NAME,ss-local,DIRECT
PROCESS-NAME,privoxy,DIRECT
PROCESS-NAME,trojan,DIRECT
PROCESS-NAME,trojan-go,DIRECT
PROCESS-NAME,naive,DIRECT
PROCESS-NAME,Thunder,DIRECT
PROCESS-NAME,DownloadService,DIRECT
PROCESS-NAME,qbittorrent,DIRECT
PROCESS-NAME,Transmission,DIRECT
PROCESS-NAME,fdm,DIRECT
PROCESS-NAME,aria2c,DIRECT
PROCESS-NAME,Folx,DIRECT
PROCESS-NAME,NetTransport,DIRECT
PROCESS-NAME,uTorrent,DIRECT
PROCESS-NAME,WebTorrent,DIRECT
DOMAIN-SET,https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/reject.txt,REJECT
RULE-SET,SYSTEM,DIRECT
DOMAIN-SET,https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/icloud.txt,DIRECT
DOMAIN-SET,https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/apple.txt,DIRECT
DOMAIN-SET,https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/google.txt,DIRECT
DOMAIN-SET,https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/proxy.txt,PROXY,force-remote-dns
DOMAIN-SET,https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/direct.txt,DIRECT
DOMAIN-SET,https://raw.githubusercontent.com/Loyalsoldier/surge-rules/release/cncidr.txt,DIRECT,no-resolve
RULE-SET,LAN,DIRECT,no-resolve
FINAL,PROXY,dns-failed
```

## 致谢

- [@Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat)
- [@v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)
- [@felixonmars/dnsmasq-china-list](https://github.com/felixonmars/dnsmasq-china-list)
- [@17mon/china_ip_list](https://github.com/17mon/china_ip_list)