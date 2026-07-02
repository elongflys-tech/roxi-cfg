# roxi-cfg

Signed client fallback-endpoint config (Ed25519). No secrets — signed public endpoint URLs only.

## proxy-domains.json — 强代理域名远程表（免发版）

sing-box **source-format rule-set**（`version: 2`）。App（builder.go 的 `roxi-proxy` 远程 rule-set，每 6h/重启刷新，经代理拉取）在「智能分流」模式下把这里列的域名**强制走代理 + 远程加密 DNS**，避免它们落到国内直连规则被 GFW 挡。

**运营加域名 = 只改 `domain_suffix` 列表推一下 main，无需发版/重打包。** 典型场景：某 Google/其它子服务在国内智能分流下连不上（如 Play 商店下载 `gvt1.com`，工单 #99）。

- 格式必须是合法 sing-box rule-set（`domain_suffix` 用**后缀**，`gvt1.com` 覆盖 `*.gvt1.com`）。
- App 内还有 hardcoded floor（核心 Google 域）作离线兜底，故此文件短暂不可达不致命。
- 生效有延迟（客户端缓存 + 6h 刷新周期），不是实时。
