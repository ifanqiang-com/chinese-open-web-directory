# 2026-11-27 全量目录巡检

完成生产公开数据、公开导出和静态数据的全量 URL 检查：1,664 个去重 URL（含来源地址及独立影视入口），另外检查 123 个加密独立栏目入口。检查普通 GET，主检查并发 8、同域串行节流，连接超时 7 秒、请求超时 22 秒，失败最多两次。补充核验 63 个目标，其中两个 CNN 路径是脚本字符串误识别，不是目录条目，不作为归档依据。

结果：新增 1、更新/规范化迁移 21、归档 0。186 个 URL 待复查，13 个上轮待复查 URL 恢复。67 个公开 YouTube 频道全部 HTTP 200。普通数据唯一 404 属于已暂停的影视入口；没有新增明确 404/410、域名失效或证书错误。连续超时没有独立停运证据，继续保留。HTTP 200 不代表全部功能或内容权利已审计。

## 新增

- [Full Stack Open 全栈公开课](https://fullstackopen.com/zh/)：赫尔辛基大学免费课程，中文正文与 React 练习可阅读；[官方课程介绍](https://fullstackopen.com/en/about/)和大学课程目录互证。需要编程基础，中文部分更新节奏不同，简介提示对照英文版。
- 同时扫描 Exercism、roadmap.sh 官方入口；未完成进一步课程和组织核验，本轮暂不添加，不凑满额。

## 更新与迁移

所有目标均由旧地址永久重定向、HTTP 200、页面 canonical 和品牌/服务一致性核验；更新 URL 及相同的来源地址。名称、分类、标签和语言逐项检查，适用字段保留。Curiosity University 简介具体化；Fountain 官网现在突出播客剪辑与推广，修正旧收听/打赏简介和标签。

| 条目 | 新官方入口 |
| --- | --- |
| Wikimedia Commons | https://commons.wikimedia.org/wiki/Main_Page |
| Curiosity University | https://www.curiosityu.com/ |
| Deno Docs | https://docs.deno.com/runtime/ |
| RPGnet Forums | https://forum.rpg.net/index.php |
| IEEE Xplore | https://ieeexplore.ieee.org/Xplore/home.jsp |
| Postman Docs | https://learning.postman.com/docs/getting-started/overview |
| Spotify Podcasts | https://open.spotify.com/genre/0JQ5DArNBzkmxXHCqFLx2J |
| Simplecast | https://www.simplecast.com |
| Wikispecies | https://species.wikimedia.org/wiki/Main_Page |
| BBC Podcasts | https://www.bbc.co.uk/sounds/podcasts |
| DW English | https://www.dw.com/en/top-stories/s-9097 |
| 德国之声中文 | https://www.dw.com/zh/%E5%9C%A8%E7%BA%BF%E6%8A%A5%E5%AF%BC/s-9058 |
| 早安健康 | https://edh.tw |
| Fountain | https://fountain.fm |
| FutureTools | https://futuretools.io |
| Numbeo | https://www.numbeo.com/cost-of-living/ |
| Open Source Alternative To | https://opensourcealternative.to |
| Podigee | https://www.podigee.com/ |
| Ribbonfarm | https://ribbonfarm.com/ |
| Wikidata | https://www.wikidata.org/wiki/Wikidata:Main_Page |
| Wikisource | https://wikisource.org/wiki/Wikisource:Main_Page |

## 保留与风险

- 语言/地区路由（DeepL、Wire、KKday、LSEG、Skillshare、Western Union、Pluto 等）不固化当前访问地区。ABC 新闻入口跳至门户，尚不足以确认新闻服务迁移，继续观察。
- 48 个短正文或无标题页面另行复核；已识别验证码、区域限制及客户端跳转。标题差异主要为版本、首页文案、定位和恢复响应；Million Short 仍为搜索服务。
- 内容政策关键词复核覆盖全部公开生产网站和频道；新闻主题、航班机场、反向代理文档、宗教文献资料不因关键词本身认定违规。本轮没有新增充分排除证据。此检查并非所有媒体资金链、所有文章或所有外部资源的完整审计。
- 独立栏目遵守既有保留授权：118 个 200、2 个 403、2 个 406、1 个 451；没有 DNS/TLS 或 404/410 错误，无新增跨域跳转。明文只保留在私有临时目录，不进入公开证据或 Git。

## 数据与验证

生产修改采用锁表事务、全量快照防并发覆盖、重复 ID 和规范化 URL 检查，回滚演练通过后提交。重新导出 JSON、CSV、URL 清单和 Markdown，并同步静态数据。更新后公开网站 1,441、频道 67。

数据/schema 校验、跨三份数据的字段及重复项核对、成人隔离与分析测试、加密目录验证、Astro 类型检查和本地静态构建均通过。依赖安装仍提示既有安全公告；本轮未修复依赖或宣称 npm audit 通过。

没有生产静态部署、密钥改动、硬删除、审批绕过或用户原工作区覆盖。逐 URL 脱敏证据见 checks.jsonl，变更见 decisions.json，汇总见 summary.json。
