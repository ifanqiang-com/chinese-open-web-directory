# 2026-11-05 全量目录质量巡检

记录时间：2026-11-05T10:14:32.861532+00:00；GitHub 账号：`zpengyu`。

- 检查全部 1,448 个公开网站、67 个频道及来源字段、静态工具/频道/指南链接，共 **1529 个不同公开 URL**；另作 9 个迁移目标和候选检查。
- 新增 1 个网站；更新 5 个网站与 1 个静态工具入口；归档 8 个网站；本轮无频道变更。
- 同步后：1,441 个公开网站、67 个频道、30 个专题。
- 上轮待复查列表中有 225 个 URL 本轮返回正常页面；本轮有 148 个仍公开 URL 留待后续复查，包含新的 Blockworks Intel 目标。

## 主要结果

- 修复科技报橘、Messari → Blockworks Intel、CEIC、Eurail → Interrail 的官方迁移，并更新对应名称、简介、标签或来源地址。静态工具区 Firefox 链接同步到品牌官网。
- Podomatic 的 www 首页两次 404，但同域不带 www 首页与收听入口正常，改为有效官方首页。
- FreewareFiles 连续两轮进入无关域名重定向链，独立历史扫描记录博彩内容，按安全和不相关内容规则归档。
- Amazon 官方说明 Freevee 已整合到 Prime Video 免费内容，归档退役独立品牌条目，保留现有 Prime Video。
- OpenStax、ICPSR 有运营方明确披露的 NSF 拨款；NPR/PBS 有官方历史联邦拨款披露。沿用上轮包含已披露历史拨款的收录排除口径。**NPR/PBS 的联邦资助已终止，本文不声称其当前仍获资助。所有资金背景归档均为站点所有者的收录政策选择，不是恶意、失效或可信度判断。**
- 新增 TypeScript 入门教程：作者官网与开源仓库双向核验，提供中文类型系统入门内容；不同于已收录的英文官方文档。Rust 语言圣经候选从 course.rs 跳转后返回 404，未新增，也未为了数量添加其他资源。
- HowHow / HowFun 官方身份一致，保持原链接。Privacy International 本轮已从临时媒体服务跳转恢复正常首页，保持原 URL。Hulu 尚有独立订阅和应用，官方仅说明整合进程，未仅凭地区/临时跳转归档。

## 方法、保留项与边界

普通 GET、HTTP/1.1、最多 8 路并发、按主域名串行、常见复合后缀归并；7 秒连接超时、22 秒单次请求超时、最多一次重试。401/403/429 不立即重试，429 对后续同域请求退避。未绕过反爬或登录；未使用证书忽略参数。检查覆盖 HTTP 状态、错误、重定向链、最终 URL、title 和 canonical，并与上轮标题及待复查记录比较。

无新增 DNS 解析失败或证书验证错误。登录/反爬/地区限制、限流、503 维护及连续超时均不自动归档；例如 DataCite、Anyway.FM、Culture Trip、NHK 和多家新闻站保留待复查，缺少停服独立证据时不把连续网络异常当作失效。公开日志删除响应重定向查询参数与片段，避免记录临时会话参数。

HTTP 200 不保证内容安全。此次为全量网络/身份元数据比对和有证据的异常/政策复核，并非逐篇审阅所有外站内容或完整机构资金审计。上轮已归档的隐藏记录不再对外请求；仅检查本轮公开内容，因此 URL 总数与上轮不同。

## 数据处理与验证

沿用上轮已确认的本机 PostgreSQL 维护库 `ifanqiang_news`：写前与上轮快照、最新仓库导出和静态数据核对一致；原 AWS RDS 已退役，未声称更新云端旧库。

- 数据库写入使用事务、表锁、完整行数与关键字段并发修改检查；写前校验 ID 和规范化 URL 唯一性，写后再次校验。先执行 ROLLBACK 演练，再 COMMIT。
- 归档只写 `status=archived, visible=false`，保留恢复快照，不硬删除数据库行。
- 重新导出 JSON、CSV、URL 列表、Markdown，并同步静态主站。
- `npm run validate`：导出、Schema、重复项检查通过。
- 维护库、公开导出和静态数据的 ID 与所有共用业务字段逐项一致。
- `npm run check`：0 errors / 0 warnings / 0 hints。
- `npm run build`：成功生成 1,642 页。
- 原有未提交改动不受影响；使用独立 worktree。未部署生产静态站，未修改密钥或权限。

## 附带发现：现有构建依赖安全公告

`npm ci` 后的 `npm audit` 报告：目录仓库 1 个 high（fast-uri）；静态仓库 13 个（1 critical、11 high、1 low）。详情与公告链接见 [dependency-findings.json](dependency-findings.json)。Astro 公告含 AVIF 图像优化 RCE，audit 提供的完整修复需要升到 Astro 7，属于独立框架升级，不混入本次内容数据 PR。当前配置是静态构建，未据此断言线上站点可被利用；需另行评估升级与实际影响。校验/类型/构建通过不等同于依赖安全审计通过。

## 逐项决策

网络证据见 [checks.jsonl](checks.jsonl)，补充检查见 [supplemental-checks.json](supplemental-checks.json)，结构化决策见 [decisions.json](decisions.json)。

| 动作 | 条目 | 原因 | 证据 |
| --- | --- | --- | --- |
| update | TechOrange 科技报橘 | 旧入口 301 跳转至新独立域名；新站 canonical 与品牌身份一致。 | [来源 1](https://buzzorange.com/techorange/)；[来源 2](https://techorange.com/) |
| update | Messari | 旧域名 301 跳转，官方收购及 Intel 上线公告明确完成平台整合；新入口反爬 429 不作为失效依据。 | [来源 1](https://blockworks.com/insights/blockworks-acquires-messari)；[来源 2](https://blockworks.com/insights/introducing-blockworks-intel) |
| update | CEIC Data | 旧站跳转至母公司 CEIC 产品页，目标 canonical 与 CEIC 登录页返回官网链接相互印证。 | [来源 1](https://isimarkets.com/ceic/)；[来源 2](https://insights.ceicdata.com/) |
| update | Eurail | 官方公告确认 2026-09-09 统一品牌；采用无欢迎片段的 canonical URL。 | [来源 1](https://community.interrail.com/news-and-announcements-39/one-brand-one-journey-welcome-to-interrail-22554)；[来源 2](https://www.interrail.com/en-int) |
| update | Podomatic | www 首页连续两次 404；同域无 www 官方首页和收听入口均返回 200，修复入口而非归档平台。 | [来源 1](https://podomatic.com/)；[来源 2](https://www.podomatic.com/landing/listen) |
| archive | FreewareFiles | 连续两轮跳转到无关的 sntssseccionv.com / kemendagri.com 域名链，已不提供原软件下载入口；独立安全扫描 2025-11-09 留有博彩内容记录。按无关内容和安全规则归档，不仅依据重定向超限。 | [来源 1](https://www.freewarefiles.com/)；[来源 2](https://gridinsoft.com/online-virus-scanner/url/freewarefiles-com) |
| archive | Amazon Freevee | Amazon 官方说明 Freevee 已并入 Prime Video 的免费内容；归档已退役的独立品牌条目，保留现有 Prime Video。 | [来源 1](https://advertising.amazon.com/resources/whats-new/unboxed-2025-amc-launches-prime-video-insights)；[来源 2](https://advertising.amazon.com/es-co/library/guides/free-ad-supported-streaming-tv) |
| archive | OpenStax | Rice 官方公告明确 OpenStax 获 NSF 9,000 万美元五年研究项目拨款；按既有政府资助排除政策归档，不是失效或安全判定。 | [来源 1](https://news.rice.edu/news/2024/rices-openstax-awarded-90m-lead-first-its-kind-nsf-research-hub-transformational-learning) |
| archive | ICPSR | 运营机构官方资料明确 ICPSR 获 NSF 3,800 万美元研究数据基础设施资助；按既有政府资助排除政策归档。 | [来源 1](https://midas.umich.edu/data-for-democracy-building-the-social-science-infrastructure-behind-better-policy/)；[来源 2](https://www.icpsr.umich.edu/sites/icpsr/about/history/timeline) |
| archive | NPR | 官方审计明确披露联邦机构及 CPB 历史拨款。沿用上轮包含已披露历史资助的排除口径；官网现说明联邦资助已终止，不能表述为当前仍获资助，也不作可信度或恶意判断。 | [来源 1](https://media.npr.org/documents/about/statements/fy2023/National%20Public%20Radio%20-%20Consolidated%20Financial%20Statements%20-%20S2322%20FINAL%20%28S%29.pdf)；[来源 2](https://contribute.npr.org/secure/stand-public-media) |
| archive | NPR Podcasts | 官方审计明确披露联邦机构及 CPB 历史拨款。沿用上轮包含已披露历史资助的排除口径；官网现说明联邦资助已终止，不能表述为当前仍获资助，也不作可信度或恶意判断。 | [来源 1](https://media.npr.org/documents/about/statements/fy2023/National%20Public%20Radio%20-%20Consolidated%20Financial%20Statements%20-%20S2322%20FINAL%20%28S%29.pdf)；[来源 2](https://contribute.npr.org/secure/stand-public-media) |
| archive | PBS NewsHour | PBS 官方资料披露联邦 Ready to Learn 拨款及公共广播资助。沿用上轮包含已披露历史资助的排除口径；2025 年资助终止情况一并注明，不表述为当前仍获资助，也不作恶意判断。 | [来源 1](https://www.pbs.org/about/about-pbs/blogs/news/pbs-2025-fact-sheet/)；[来源 2](https://www.pbs.org/video/may-6-2025-pbs-news-hour-full-episode-1746504001/) |
| archive | PBS Video | PBS 官方资料披露联邦 Ready to Learn 拨款及公共广播资助。沿用上轮包含已披露历史资助的排除口径；2025 年资助终止情况一并注明，不表述为当前仍获资助，也不作恶意判断。 | [来源 1](https://www.pbs.org/about/about-pbs/blogs/news/pbs-2025-fact-sheet/)；[来源 2](https://www.pbs.org/video/may-6-2025-pbs-news-hour-full-episode-1746504001/) |
| add | TypeScript 入门教程 | 作者官网与开源仓库双向确认，公开可读、上线多年且对中文初学者有明确价值；ID、域名和规范化 URL 均无重复。 | [来源 1](https://ts.xcatliu.com/)；[来源 2](https://github.com/xcatliu/typescript-tutorial) |
| update | Firefox | Mozilla 旧官方入口 301 跳转至 Firefox 品牌官网，目标普通 GET 200。 | [来源 1](https://www.mozilla.org/firefox/)；[来源 2](https://www.firefox.com/) |
