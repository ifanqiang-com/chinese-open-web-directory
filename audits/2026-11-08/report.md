# 2026-11-08 全量目录质量巡检

记录时间：2026-11-08T10:10:11.200903+00:00；GitHub 账号：`zpengyu`。

检查全部 1,441 个公开网站、67 个 YouTube 频道及来源字段、静态数据中的链接，共 **1522 个不同 URL**；另检查 11 个候选和核验 URL。
本轮新增 1、更新 2（含 Git 文档入口迁移 1）、归档 0；同步后有 1442 个网站、67 个频道。
上轮待复查 URL 中 11 个恢复正常响应；本轮 161 个 URL 保留待复查。

## 决策及证据

| 动作 | 条目 | 原因 | 证据 |
| --- | --- | --- | --- |
| update | Whoogle Search | 官方 README 明确搜索功能已失效且维护终止，GitHub 标记为归档仓库。仓库本身仍可经官方 API 读取；按严格失效归档门槛保留历史代码资料，纠正原条目仍可用的描述和搜索分类，不把本轮 504 当作永久失效。 | [来源 1](https://github.com/benbusby/whoogle-search#readme)；[来源 2](https://api.github.com/repos/benbusby/whoogle-search) |
| update | Git Documentation | 旧 /doc 页面已成为 HTML meta refresh 跳转页，canonical 指向 /docs；官方 Reference 导航和新页面内容共同确认。采用 HTTPS 直接入口并明确命令参考用途。 | [来源 1](https://git-scm.com/doc)；[来源 2](https://git-scm.com/docs) |
| add | OI Wiki | 官网、关于页、数据结构页面与官方 GitHub 仓库相互核验；仓库创建于 2018 年、2026-11-07 仍有更新。中文竞赛算法资料公开可读，ID、规范化 URL、域名及品牌无重复，未发现命中排除政策的证据。 | [来源 1](https://oi-wiki.org/)；[来源 2](https://oi-wiki.org/intro/about/)；[来源 3](https://oi-wiki.org/ds/)；[来源 4](https://github.com/OI-wiki/OI-wiki) |

## 异常复核与保留项

- Whoogle 官方 README 披露搜索功能永久不可用、维护终止，仓库自身仍可从官方 API 读取。本轮将条目明确标为历史源码并调整简介、分类和标签，不再当作可用搜索工具推荐；不因一次 GitHub 504 或仓库只读状态直接归档。
- GitHub 多个无关项目页面本轮均返回 504；age 官方 API 显示项目未归档，保留待复查。
- DataCite 仍有连接错误，但官方 [活动页](https://datacite.org/events/)列有近期和即将举行的活动，缺少停服证据，保留。Svbtle 和 MacPorts 本轮恢复正常首页。
- Curiosity U / Curiosity University 仍是相同域名与服务；Kagi、WordPress 的标题微调和 SearXNG 文档版本更新不构成迁移。
- YouTube 频道均已检查页面标题/身份；没有频道变更。地区、登录、限流和反爬响应不作为失效证据，不固化地区、登录或版本重定向 URL。

## 方法与边界

普通 GET、HTTP/1.1、最多 8 路并发、同主域名串行、7 秒连接超时、22 秒请求超时、最多一次重试；401/403/429 不立即重试，429 对后续同域请求退避。不忽略 TLS 验证，不绕过登录或反爬。记录状态、错误、跳转链、最终 URL、title、canonical，并对比上轮记录。另抽查短响应/空标题页，发现 Git 文档的 HTML 跳转；Stooq/HappyCow 的浏览器验证与空响应均记为待复查。公开日志省略响应 URL 的查询参数和片段。

这是全量网络与身份元数据巡检，加上异常、候选和内容政策复核；不是逐篇外站正文审阅、完整资金关系审计或安全背书。HTTP 200 不等于安全。

## 数据与验证

- 沿用已确认的本机 PostgreSQL 维护数据源；原云 RDS 已退役。写前与上轮快照、最新公开导出及静态数据逐字段一致。
- 独立 worktree；事务、表锁、并发修改检查、ID 与规范化 URL 重复检查；先 ROLLBACK 演练，再 COMMIT。保留前后快照，不做硬删除。
- 重新导出 JSON、CSV、URL 列表和 Markdown，并同步静态主站数据。
- 数据/Schema/重复检查通过，数据库、导出与静态共用字段一致。
- Astro 类型检查及静态构建通过；详情见 PR 验证摘要。
- 已报告的依赖安全公告与上轮逐项相同：目录 1 high，静态 1 critical / 11 high / 1 low；未在本轮扩展框架升级范围。检查与构建通过不代表依赖安全审计通过。
- 未执行生产静态站部署，未修改密钥或权限，未覆盖原工作区改动。

结构化记录：[summary.json](summary.json)、[checks.jsonl](checks.jsonl)、[supplemental-checks.json](supplemental-checks.json)、[decisions.json](decisions.json)。
