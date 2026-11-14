# 2026-11-14 全量目录质量巡检

记录时间：2026-11-14T10:10:28.743175+00:00；GitHub 账号：`zpengyu`。

检查原有 1,438 个公开网站、67 个 YouTube 频道及来源字段、静态数据链接，共 **1521 个不同 URL**；另检查 24 个证据、候选与补充 URL。
本轮新增 1、更新 4（含 TED 官方迁移及 OpenAPI canonical 更新）、归档 3；同步后为 1436 个网站和 67 个频道。
上轮待复查中 9 个恢复；本轮 153 个 URL 留待复查。

## 决策与证据

| 动作 | 条目 | 原因 | 证据 |
| --- | --- | --- | --- |
| archive | OnionShare | 维护者公告及项目安全公告确认，2021 年项目安全审计由 OTF Red Team Lab 资助；按既有美国政府资助排除口径归档。此为历史审计支持，不表示当前拨款或当前软件不安全。 | [来源 1](https://micahflee.com/onionshare-25-released/)；[来源 2](https://github.com/onionshare/onionshare/security/advisories/GHSA-ch22-x2v3-v6vq)；[来源 3](https://www.usagm.gov/networks/otf/) |
| archive | Citizen Lab | 项目方 2020 年说明：不接受直接政府拨款，但 OTF 通过研究员项目及 Citizen Lab Summer Institute 提供支持；按既有实质资金支持排除口径归档，不将研究员资助表述为实验室直接政府拨款。 | [来源 1](https://citizenlab.ca/keep-the-open-technology-fund-open/)；[来源 2](https://www.usagm.gov/networks/otf/) |
| archive | Amtrak | Amtrak 2026-11-09 官方公告明确芝加哥联合车站项目获得美国国会拨款及 FRA 联邦补助；按美国政府资金支持排除规则归档，不表示其服务失效或不安全。 | [来源 1](https://media.amtrak.com/2026/11/amtrak-to-start-construction-of-new-boarding-platforms-at-chicago-union-station/) |
| update | TED Podcasts | 旧官方入口发布迁移通知并以 JavaScript 跳转至 TED Podcasts；新页面 canonical 一致，并包含 TED 中文节目入口。保留原 ID，同步名称、URL、简介、标签、语言及来源地址。 | [来源 1](https://audiocollective.ted.com/)；[来源 2](https://www.ted.com/podcasts)；[来源 3](https://www.ted.com/podcasts/tedinchinese) |
| update | Apple TV | Apple 官方产品页与当前播放入口已使用 Apple TV 名称；修正旧 Apple TV+ 名称及简介，保留官方播放地址和分类。 | [来源 1](https://www.apple.com/apple-tv/)；[来源 2](https://tv.apple.com/) |
| update | OpenAPI Initiative | 原 www 官网现 301 至根域，新页面 canonical 为 https://openapis.org/；同步 URL 与来源地址。 | [来源 1](https://www.openapis.org/)；[来源 2](https://openapis.org/) |
| update | 民报 | 官方首页现明确以财经及生活新闻为重点；更新过于笼统的简介和评论标签，网址、名称及中文新闻分类保持适用。 | [来源 1](https://www.peoplenews.tw/) |
| add | Learn Git Branching | 2012 年创建且持续维护的 MIT 开源 Git 可视化教程；官方仓库 CNAME 验证域名归属，浏览器实测简体中文关卡与界面可用。无重复 ID、规范化 URL 或同品牌记录。 | [来源 1](https://learngitbranching.js.org/)；[来源 2](https://github.com/pcottle/learnGitBranching)；[来源 3](https://github.com/pcottle/learnGitBranching/blob/main/CNAME)；[来源 4](https://github.com/pcottle/learnGitBranching/blob/main/src/levels/intro/commits.js) |

## 复核结论

- 未发现已确认的 404/410、DNS 失效、证书验证失败或劫持证据。重复超时、反爬、登录、限流均保留复查，不因连续网络失败直接归档。
- TED 原站是 HTTP 200 的迁移通知和 JavaScript 跳转，新官方页面的 canonical 一致。同步名称、网址、简介、标签、语言、来源，分类仍为播客与音频。
- Apple 官方产品页和播放入口使用 Apple TV 品牌；修正旧 Apple TV+ 名称与简介，不修改播放 URL。
- 三个资金政策归档项不等同于失效、恶意或低质量。Amtrak 有当前官方联邦项目补助公告；OnionShare 是历史审计资金；Citizen Lab 明确不接受直接政府拨款，官方证据是 OTF 研究员及活动支持。按既有实质资金支持口径处理，未声称历史资助持续至今。
- 本轮查看的 Access Now、RSF 官方资金说明不足以确认美国政府资助，不凭组织立场或仅有非美国政府资金归档。
- 已检查全部频道 URL 和页面身份变化，频道无改动。Libsyn 文案、SearXNG/Node.js 版本、N26/CNBC/LinkedIn/WeTV 地区或语言变化不构成迁移。
- ChemRxiv、Wiley 的 HTTP 200 为 cookie 提示，仍列待复查；Roku、Debian 论坛、Project Euclid、Stooq、PNAS 等不把 HTTP 200 单独当作内容正常。
- HappyCow 短响应经补充请求恢复正常餐厅目录内容，保留收录。
- HTML refresh 的目标额外检查；稳定文档入口不固定到 PyTorch 等具体版本。

## 候选筛选

- Learn Git Branching：新增。官方源码、CNAME、历史及中文内容核验通过，浏览器实测可用；与已收录 Git 官方文档用途不同，无同品牌重复。证据：[来源](https://learngitbranching.js.org/)、[来源](https://github.com/pcottle/learnGitBranching)
- Full Stack Open 中文：继续暂缓。官方公告仍说明平台迁移中，第 6 部分起仅提供英文；不为凑数新增。证据：[来源](https://fullstackopen.com/zh/new-platform/)

## 方法与验证

- 普通 GET、最多 8 路并发、同主域串行、7 秒连接/22 秒请求超时、最多一次重试；401/403/429 不立即重试，429 同域退避，不绕过 TLS、登录或反爬。补充核验最多 2 路并发。
- 保存 HTTP 状态、错误、重定向链、最终 URL、title、canonical，并与上轮比较；抽查短响应和 HTML 跳转。公开响应 URL 去除查询参数和片段。
- 覆盖全部公开 URL 的网络和身份元数据、异常及内容政策复核，不代表逐篇审阅外站文章或完成所有机构资金关系审计。
- 干净 worktree 保留用户改动；维护 PostgreSQL 数据源与上轮快照及最新仓库一致。事务加表锁、并发修改保护、ID/规范化 URL 去重，先 ROLLBACK 演练再 COMMIT；归档设为 archived、visible=false。
- 重导 JSON、CSV、URL 清单、Markdown 并同步静态数据；数据/schema/重复项检查及 DB/导出/静态字段一致性验证通过。Astro 类型检查和静态构建结果见 PR。
- npm audit 的受影响包计数为目录 1 high、静态 1 critical / 11 high / 1 low；计数相同，但新检出 2 条 Astro 公告。
- [GHSA-mh32-jxcr-mh9f](https://github.com/advisories/GHSA-mh32-jxcr-mh9f)：动态标签名注入；本仓库未使用不可信数据作为标签名。[GHSA-r3h5-4585-7x3w](https://github.com/advisories/GHSA-r3h5-4585-7x3w)：需要 Node adapter 按需图片端点；本仓库为默认静态输出且无此 adapter。基于代码检查未发现这两项触发条件，不表示所有依赖安全；既有依赖升级仍是后续维护工作。
- 不执行生产静态部署，不修改密钥、权限或分支保护。

结构化记录：[summary.json](summary.json)、[checks.jsonl](checks.jsonl)、[supplemental-checks.json](supplemental-checks.json)、[decisions.json](decisions.json)、[security-review.json](security-review.json)。
