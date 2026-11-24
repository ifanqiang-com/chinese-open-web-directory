# 2026-11-24 全量目录巡检

账号 zpengyu；隔离 worktree；保留用户原有未提交改动。

- 检查生产、公开导出和静态数据的全部 1,662 个不同入口/来源 URL（含一个已暂停影视入口），另检查当前独立栏目的 123 个 URL。
- 新增 2：[Flexbox Froggy](https://flexboxfroggy.com/) 和 [Grid Garden](https://cssgridgarden.com/)。作者 Thomas Park / Codepip、官方源码互链、中文关卡和练习判定逻辑已核验。官网有广告及商业会员入口，核心是原创课程，并非联盟空壳；未发现明确政策排除证据。浏览器环境不可用，未进行交互试玩；不声称完成全部课程或全面资金审计。
- 更新/迁移 1：[声动活泼](https://www.shengfm.cn/)。旧域名 301 至 www，官方 canonical 相符，独立网页读取核验品牌与节目；同步网址、来源和简介。后续一次补充请求超时，保留其可用性待复查，不以偶发失败否定已核验迁移。
- 归档 0；普通目录未发现确认的 404/410、DNS/TLS 错误或明显劫持。已暂停的影视入口仍 404，未重新公开。67 个 YouTube 频道均 HTTP 200。
- 192 个主清单 URL 待复查，上轮待复查中 13 个恢复。对反爬、登录、限流、地区限制和重复超时不直接归档。NHK 仍超时，没有独立关闭证据；MarketScreener、Yep 等复核为拦截页。
- 比较本轮与上轮标题、跳转和 canonical，并复核 49 个短/无标题响应。SearXNG 版本、Hostelz 数量、播客页面文案等正常更新未改目录；Google Travel unsupported 页面未用作迁移目标。
- 独立栏目仅报告风险，123 个链接中 119 HTTP 200、1 HTTP 403、2 HTTP 406、1 HTTP 451，未发现 DNS/TLS 失败。保留授权内容与密文。没有发布任何独立目录名称、网址、明文或密钥；第三方 DNS 复核被自动审批拒绝且未执行，本轮无 DNS 失败亦无需进一步复核。
- GET 并发 8，同主域串行，连接 7 秒/请求 22 秒超时，最多一次重试，401/403/429 不即时重试；独立和补充检查并发 2。公开证据去除查询参数；完整原始记录仅保存在本地。
- 数据修改使用锁定事务、完整快照并发检查、ID/规范化 URL 去重，先回滚演练再提交，无硬删除。重新导出 JSON、CSV、URL 和 Markdown，并同步静态普通数据。最终 1,440 网站、67 频道。
- 数据/schema、三处字段一致性、重复项检查通过；现有成人/分析测试、加密目录校验、类型检查、静态构建通过。不部署生产站，不改变密钥、权限或审批要求。

来源：[Flexbox 官方源码](https://github.com/thomaspark/flexboxfroggy)、[Grid 官方源码](https://github.com/thomaspark/gridgarden)、[Codepip 介绍](https://codepip.com/about/)、[商业模式 FAQ](https://codepip.com/faq/)。
