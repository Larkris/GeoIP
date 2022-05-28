# 简介

精简版 GeoIP，Forked From [Loyalsoldier/geoip](https://github.com/Loyalsoldier/geoip)，本项目每天早上7点、晚上7点自动生成 MaxMind mmdb 格式文件`Country.mmdb`，仅包含CN地区的IP数据。

[![Build Country.mmdb](https://github.com/Larkris/GeoIP/actions/workflows/main.yml/badge.svg)](https://github.com/Larkris/GeoIP/actions/workflows/main.yml)

> IPV4数据: 来自[Clang.CN](https://ispip.clang.cn/all_cn.txt)、[纯真CN数据库](https://raw.githubusercontent.com/metowolf/iplist/master/data/special/china.txt)、[IPIP.net](https://raw.githubusercontent.com/17mon/china_ip_list/master/china_ip_list.txt)。

> IPV6数据: 来自[Clang.CN](https://ispip.clang.cn/all_cn_ipv6.txt)、[中国运营商IP地址库](https://raw.githubusercontent.com/gaoyifan/china-operator-ip/ip-lists/china6.txt)。

> IPV4数据插入顺序：Clang.CN ➟ 纯真CN数据库 ➟ IPIP.net。

> IPV6数据插入顺序：Clang.CN ➟ 中国运营商IP地址库。

### 下载地址

> 适用于 Surge、Quantumult X、Clash。

- [下载地址](https://github.com/Larkris/GeoIP/raw/release/Country.mmdb)

## 定制 GeoIP 文件

可通过以下几种方式定制 GeoIP 文件：

- **在线生成**：[Fork](https://github.com/Loyalsoldier/geoip/fork) 本仓库后，修改自己仓库内的配置文件 `config.json` 和 GitHub Workflow `.github/workflows/build.yml`

**特别说明：**

- **在线生成**：[Fork](https://github.com/Loyalsoldier/geoip/fork) 本项目后，如果需要使用 MaxMind GeoLite2 Country CSV 数据文件，需要在自己仓库的 **[Settings]** 选项卡的 **[Secrets]** 页面中添加一个名为 **MAXMIND_GEOLITE2_LICENSE** 的 secret，否则 GitHub Actions 会运行失败。这个 secret 的值为 MAXMIND 账号的 LICENSE KEY，需要[**注册 MAXMIND 账号**](https://www.maxmind.com/en/geolite2/signup)后，在[**个人账号管理页面**](https://www.maxmind.com/en/account)左侧边栏的 **[Services]** 项下的 **[My License Key]** 里生成。

### 概念解析

本项目有两个概念：`input` 和 `output`。`input` 指数据源（data source）及其输入格式，`output` 指数据的去向（data destination）及其输出格式。CLI 的作用就是通过读取配置文件中的选项，聚合用户提供的所有数据源，去重，将其转换为目标格式，并输出到文件。

### 支持的格式

关于每种格式所支持的配置选项，查看本项目 [`config-example.json`](https://github.com/Loyalsoldier/geoip/blob/HEAD/config-example.json) 文件。

支持的 `input` 输入格式：

- **text**：纯文本 IP 和 CIDR（例如：`1.1.1.1` 或 `1.0.0.0/24`）
- **private**：局域网和私有网络 CIDR（例如：`192.168.0.0/16` 和 `127.0.0.0/8`）
- **cutter**：用于裁剪前置步骤中的数据
- **v2rayGeoIPDat**：V2Ray GeoIP dat 格式（`geoip.dat`）
- **maxmindGeoLite2CountryCSV**：MaxMind GeoLite2 country CSV 数据（`GeoLite2-Country-CSV.zip`）
- **clashRuleSetClassical**：[classical 类型的 Clash RuleSet](https://github.com/Dreamacro/clash/wiki/premium-core-features#classical)
- **clashRuleSet**：[ipcidr 类型的 Clash RuleSet](https://github.com/Dreamacro/clash/wiki/premium-core-features#ipcidr)
- **surgeRuleSet**：[Surge RuleSet](https://manual.nssurge.com/rule/ruleset.html)

支持的 `output` 输出格式：

- **text**：纯文本 CIDR（例如：`1.0.0.0/24`）
- **v2rayGeoIPDat**：V2Ray GeoIP dat 格式（`geoip.dat`，适用于 [V2Ray](https://github.com/v2fly/v2ray-core)、[Xray-core](https://github.com/XTLS/Xray-core) 和 [Trojan-Go](https://github.com/p4gefau1t/trojan-go)）
- **maxmindMMDB**：MaxMind mmdb 数据格式（`GeoLite2-Country.mmdb`，适用于 [Clash](https://github.com/Dreamacro/clash) 和 [Leaf](https://github.com/eycorsican/leaf)）
- **clashRuleSetClassical**：[classical 类型的 Clash RuleSet](https://github.com/Dreamacro/clash/wiki/premium-core-features#classical)
- **clashRuleSet**：[ipcidr 类型的 Clash RuleSet](https://github.com/Dreamacro/clash/wiki/premium-core-features#ipcidr)
- **surgeRuleSet**：[Surge RuleSet](https://manual.nssurge.com/rule/ruleset.html)

## License

[CC-BY-SA-4.0](https://creativecommons.org/licenses/by-sa/4.0/)

This product includes GeoLite2 data created by MaxMind, available from [MaxMind](http://www.maxmind.com).
