# 2026-11-11 全量目录质量巡检

记录时间：2026-11-11T10:09:12.460036+00:00；GitHub 账号：`zpengyu`。

检查原有 1,442 个公开网站、67 个 YouTube 频道及来源字段、静态数据链接，共 **1523 个不同 URL**；另检查 21 个证据、候选与补充 URL。
本轮新增 1、更新 1（含 Roku 官方迁移 1）、归档 5；同步后为 1438 个网站和 67 个频道。
上轮待复查中 10 个恢复；本轮 161 个 URL 留待复查。

## 决策与证据

| 动作 | 条目 | 原因 | 证据 |
| --- | --- | --- | --- |
| archive | Zotero | Zotero 官方资助致谢确认曾获美国联邦机构 IMLS 支持，项目原开发机构亦确认早期拨款；依既有历史资助排除口径归档。官方当前说明开发及运营由个人和机构存储订阅收入支持，不声称目前仍受政府资助，也不认定软件不安全。 | [来源 1](https://www.zotero.org/support/credits_and_acknowledgments)；[来源 2](https://20.rrchnm.org/exhibits/show/ooh/funding.html)；[来源 3](https://www.zotero.org/getinvolved) |
| archive | Stanford Encyclopedia of Philosophy | 官方 History of Grants 列出 NEH、NSF 对本项目的多笔历史拨款（1998—2008），按目录资金来源排除政策归档；不是链接失效或内容质量判断。 | [来源 1](https://plato.stanford.edu/about.html)；[来源 2](https://www.neh.gov/news/press-release/2000-09-28) |
| archive | DPLA | IMLS 官方公告确认 2014 年向 DPLA 提供 999,485 美元用于扩展基础设施，且此前于 2012 年拨款；DPLA 自身公告也确认 Open eBooks 的 IMLS 支持。依目录资金来源政策归档；这是历史资助证据，不声称当前仍获此拨款。 | [来源 1](https://www.imls.gov/news/new-imls-funding-support-digital-public-library-america)；[来源 2](https://dp.la/news/open-ebooks-opens-world-of-digital-reading-to-children) |
| archive | Signal | OTF 官方项目页列出 2013—2016 年向 Signal/Open Whisper Systems 提供的历史资金共 2,955,000 美元，并明确项目状态 Inactive；USAGM 官方介绍确认其与 OTF 的资助体系。按目录历史资助排除口径归档，不声称 Signal 当前受资助或不安全。 | [来源 1](https://www.opentech.fund/projects-we-support/supported-projects/signal-open-whisper-systems/)；[来源 2](https://www.usagm.gov/networks/otf/) |
| archive | Perseus Digital Library | NEH 官方项目介绍及 2017 年专题确认 Perseus 获得 11 笔 NEH 拨款，共 1,162,653 美元。按目录历史资助排除政策归档，不以 HTTP 响应或资源质量为理由。 | [来源 1](https://www.neh.gov/project/perseus-project)；[来源 2](https://www.neh.gov/humanities/2017/fall/feature/how-do-you-get-students-study-ancient-greek-modern-campus) |
| update | Roku App | 原 The Roku Channel 网页入口返回 301，新入口 canonical 为 app.roku.com；Roku 官方产品页与支持文档共同确认更名及迁移。同步名称、URL、来源、简介与标签，保留原分类、英语及有 App 字段。地区限制或临时错误不作为失效依据。 | [来源 1](https://therokuchannel.roku.com/)；[来源 2](https://app.roku.com/)；[来源 3](https://www.roku.com/roku-app)；[来源 4](https://support.roku.com/article/get-the-roku-channel) |
| add | tldr pages | 官网、官方 GitHub 仓库及简体中文 tar/git 页面互相核验。项目创建于 2013-12-08，本轮仍活跃，公开可读且提供中文实例；ID、规范化 URL、域名和品牌均无重复，未发现排除政策证据。 | [来源 1](https://tldr.sh/)；[来源 2](https://github.com/tldr-pages/tldr)；[来源 3](https://github.com/tldr-pages/tldr/blob/main/pages.zh/common/tar.md)；[来源 4](https://github.com/tldr-pages/tldr/blob/main/pages.zh/common/git.md) |

## 复核结论

- 没有确认的 404/410、域名解析失败、证书验证失败或劫持证据。单次或重复超时、反爬、登录、限流不能单独作为归档理由。
- 5 个资金政策排除项均有项目方或拨款方一手证据。归档遵循本目录既有历史资助口径，不把历史支持写成当前拨款，也不将资金来源等同于恶意软件或低质量内容。Zotero 官方现说明运营由存储订阅收入支持；Signal 的 OTF 项目状态为 Inactive。
- Roku 旧入口 301、新入口 canonical、官方产品页和支持文档相互印证，更新名称、网址、来源、简介及地区限制标签。网页可返回临时/地区错误，迁移确认不代表所有地区均可播放。
- 67 个频道均检查标题和身份，未发现需变更频道。GitHub 的 5 个上轮 504 页面本轮恢复；Whoogle 继续保留准确的历史源码说明。
- Curiosity、PubPeer、Podpage 标题变化，N26/CNBC/LinkedIn 地区或语言变化，不构成身份迁移。PyTorch stable 的 HTML 跳转保留稳定入口，不固定到具体版本。
- HappyCow 本轮恢复正常内容；Debian 论坛 Anubis、Project Euclid Incapsula、SEDAR+ Radware、PNAS cookie 页面和 Stooq JS 验证均保留待复查。

## 候选筛选

- 新增 tldr pages：2013 年起维护，官方仓库仍活跃，简体中文 tar/git 页面已核验，提供明确的命令行学习价值。
- Full Stack Open 中文官方公告正迁移平台，部分章节目前只有英文；本轮暂不新增，后续再核验稳定入口。

## 方法与验证

- 普通 GET、最多 8 路并发、同主域串行、7 秒连接/22 秒请求超时、最多一次重试；401/403/429 不立即重试，429 同域退避，不绕过 TLS、登录或反爬。补充核验最多 2 路并发。
- 保存 HTTP 状态、错误、重定向链、最终 URL、title、canonical，并与上轮比较。抽查短响应及 HTML 跳转。公开响应 URL 去除查询参数和片段。
- 这是全部公开 URL 的网络与身份元数据巡检、异常及内容政策复核，并非逐篇外站文章审阅或完整资金关系审计。
- 使用干净 worktree；原用户改动未变。维护 PostgreSQL 数据源与上轮快照和最新仓库逐字段一致。
- 事务加表锁、并发修改保护、ID/规范化 URL 去重，先 ROLLBACK 演练再 COMMIT；归档设为 archived、visible=false，保留原记录。
- 重导 JSON、CSV、URL 清单、Markdown，静态数据同步；数据/schema/重复项检查及 DB/导出/静态一致性验证通过。Astro 类型检查和构建通过，具体数量见 PR。
- 依赖公告逐项与上轮相同：目录 1 high；静态 1 critical、11 high、1 low。本轮不重复报告既有漏洞，不将类型/构建成功描述为依赖安全审计通过。
- 不执行生产静态部署，不修改密钥、权限或分支保护。

结构化记录：[summary.json](summary.json)、[checks.jsonl](checks.jsonl)、[supplemental-checks.json](supplemental-checks.json)、[decisions.json](decisions.json)。
