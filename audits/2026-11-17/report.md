# 2026-11-17 全量目录巡检

使用 `zpengyu`；从最新默认分支创建独立 worktree，保留原工作区未提交改动。
检查 1,437 个普通网站、67 个 YouTube 频道及来源字段与静态数据，共 1,553 个不同 URL（包括影视栏目中已暂停、未公开的 1 个 URL）；另检查独立栏目 70 个公开 URL，以及 19 个候选与补充 URL。
本轮新增 1 项，更新、迁移、归档均为 0。完成后普通目录为 1,438 个网站、67 个频道、30 个专题。171 个主清单 URL 留待复查，上轮待复查中 1 个恢复。

## 新增

- [Regex Learn 中文版](https://regexlearn.com/zh-cn)：免费开源的正则表达式分步课程、语法备忘单和在线测试工具。按中文入口设为 `zh`，归入开发者资源。
- [官方仓库](https://github.com/aykutkardas/regexlearn.com)于 2021-08-28 创建，2026-10 仍有维护；官方站与仓库相互链接，中文版、课程、备忘单、游乐场均返回 200。浏览器确认简体中文 56 步课程正常渲染，无需登录。
- 检查[公开赞助列表](https://github.com/aykutkardas/regexlearn.com/blob/main/sponsors.json)，未发现符合本轮资金或内容排除规则的证据；这不是全面资金审计。
- [Flexbox Froggy](https://flexboxfroggy.com/)保留为后续候选：官方页面可访问，本轮未完成中文版本及维护来源深入核验；不为凑数添加。

## 原有条目复核

- 普通目录无确认的 404/410、DNS/TLS 失效或劫持证据；全部 67 个频道返回 200，页面身份无明显变化。
- 影视数据中已暂停的 URL 仍返回 404，没有重新公开。其余影视条目按用户授权保留；访问受限与版权风险不等同于已确认恶意或获得版权认证。
- Bitbucket、Curiosity Stream、SolidJS、Open Food Facts、Hostelz、Udemy 的变化属于文案；SearXNG 是版本更新；LinkedIn、WeTV 是地区/语言切换，不据此迁移条目。
- 短响应和无标题页额外检查 42 项；页面内文档跳转目标均已核查。保留 PyTorch 等稳定文档 URL，未固定到版本路径。
- AppImage 与 CNN 首次空响应经补充请求恢复；Trove 仍为反爬挑战，不计作恢复。Wiley/ChemRxiv cookie 提示、Stooq、Debian、Project Euclid、PNAS、Roku 等仍列待复查。NHK 等重复超时没有独立关闭证据，保留。

## 独立栏目：按用户确认仅报告风险

- 本轮用户明确确认：保留近期授权的独立成人、影视栏目，仅报告风险。该例外不扩展至普通目录或未来新增来源。
- 独立栏目 70 个公开 URL：63 个返回 200，2 个 403，2 个 406，1 个超时，2 个解析失败。后两者的链接域名及主域名均被 Cloudflare 与 Google 公共 DNS 独立确认为 NXDOMAIN。
- 未修改独立栏目数据。两个暂存归档状态已在提交前撤回，加密源与本轮基线完全一致。失败记录及 DNS 原始证据仅保存在本地受限临时目录，不公开站名、网址或密钥。
- HTTP 200 仅表示响应，不是内容安全、权属或可持续运营保证；本轮没有逐项审查成人内容或鉴定影视授权。

## 验证与边界

- GET 最多 8 路并发，同主域串行，7 秒连接/22 秒请求超时，最多重试一次。401/403/429 不立即重试，限流退避；补充及独立栏目最多 2 路并发。不绕过证书检查、登录或反爬。
- 记录 HTTP、curl 错误码、跳转链、最终 URL、title、canonical 与检查时间。公开记录去除响应查询参数/片段，不发布原始响应或配置。
- 数据源为既有维护中的本地 PostgreSQL。事务加表锁，检查快照并发变更及 ID/规范化 URL 重复，先回滚演练再提交新增。未硬删除任何记录。
- 重导 JSON、CSV、URL 清单与 Markdown，同步静态站数据；数据库/导出/静态公共字段一致。数据/schema/重复项检查通过。静态测试、加密防泄漏检查、类型检查与构建见 PR 验证结果。
- 依赖安全公告与 11 月 14 日相同：目录 1 high；静态 1 critical、11 high、1 low。既有依赖升级仍未完成，不把 npm audit 记为通过。
- 未部署生产静态站、修改密钥、变更权限或绕过审批。网络审查不是逐篇外站内容审查或全面机构资金审计。

结构化证据：[summary.json](summary.json)、[checks.jsonl](checks.jsonl)、[supplemental-checks.json](supplemental-checks.json)、[decisions.json](decisions.json)、[independent-directory-summary.json](independent-directory-summary.json)、[security-review.json](security-review.json)。
