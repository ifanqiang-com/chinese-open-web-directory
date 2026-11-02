# 2026-11-02 全量目录巡检

记录时间：2026-11-02T10:15:59.147879+00:00。GitHub 操作账号：`zpengyu`。

- 全量请求检查：1597 个去重 URL，来自 1,512 个维护库网站、69 个频道，以及公开导出、静态数据和来源字段。
- 新增：2 个网站；更新：51 个条目（35 个网站、16 个频道）；归档：68 个条目（66 个网站、2 个频道）。
- 归档数包含此前仅在公开导出中排除的 KKTV、澳洲新快网；本轮补齐维护库与静态主站状态。
- 同步后的公开数据：1,448 个网站、67 个频道、30 个专题。
- 361 个 URL 留待复查；包含反爬、登录、地区限制、限流和临时连接异常，不据此直接归档。

## 方法与边界

普通 GET、最多 8 路并发、同主机串行、7 秒连接与 22 秒请求超时；非成功响应最多重试一次。HTTP/2 协议异常另用 HTTP/1.1 验证。Stack Exchange 返回的 429 保留待复查，下轮应按主域名限速并对 429 退避。未绕过反爬或登录。结果 JSONL 记录状态、最终地址、标题、canonical 与尝试结果；重定向查询参数从公开日志中省略。HTTP 200 也可能是验证页或错误账号，不能视为内容审查通过。

首次巡检建立可比较基线；没有把同一轮两次失败算成连续两轮失败。安全归档以当前页面或独立公开证据为依据。所有资金背景归档均是站点所有者的收录政策选择，不是对这些资源的可信度或安全性的负面结论。机构资助材料包含明确注明的历史拨款。

原部署配置中的 AWS RDS 已不存在（当前账户 us-west-2 实例列表为空，且本机留有删除前归档）。本轮使用与最新公开导出逐项匹配的本机 PostgreSQL 维护库 `ifanqiang_news`；未声称修改了已退役的云数据库。两处既有 URL 覆盖及两处排除记录已落实到维护库，清空已消费的覆盖项。

数据库写入使用事务和表锁；写前对照完整快照检查并发改动，校验原始 ID/规范化 URL 唯一性，写后再次校验全部公开数据。归档只写 `status=archived, visible=false`，未删除数据库行；本机保存修改前快照。

## 需要关注的发现

- GetMacApps 现为博彩推荐页，已从公开目录与静态数据移除。
- 多个 YouTube handle 指向无关账号或错误的频道版本，16 条已用核验后的稳定频道 ID 修正；罗翔条目未找到可信官方替代链接，归档其错误入口。
- 新增 Hello 算法和现代 JavaScript 教程；官网与长期维护的开源项目交叉验证。MDN 已有同源条目，不重复新增；未添加仅靠聚合转载证明质量的候选。
- 部分官方文档会跳转到当前版本、登录入口或地区首页，这些不自动固化为目录 URL。Privacy International 临时跳转到媒体服务、Messari 转向 Blockworks 的品牌归属仍需进一步确认，暂保留原入口。

## 验证

- `npm run validate`：导出、JSON Schema 与重复检查通过。
- `npm run check`：0 errors / 0 warnings。
- `npm run build`：成功生成 1,649 个静态页面。
- 静态数据与公开 JSON 的全部 ID、名称、URL、分类、简介、标签、语言及其他现有字段逐项一致。
- 新增和修改目标 URL 另作 GET 复核（见 [changed-url-checks.json](changed-url-checks.json)）：43/47 返回 200，HBO Max、DIRECTV、Financial Modeling Prep 与 Hello 算法复核时出现 403/429/超时；此前初检或独立官网来源可确认身份，保留并列入下轮复查。
- 导出脚本修复 README 更新逻辑，保留中文项目定位，刷新徽章和计数。
- 未部署生产静态站；线上仍需按正常发布流程上线这些仓库改动。

## 条目决策

完整机器记录见 [decisions.json](decisions.json)，网络记录见 [checks.jsonl](checks.jsonl)。

### 新增

| 条目 | ID | 原因 | 证据 / 新入口 |
| --- | --- | --- | --- |
| Hello 算法 | hello-algo-com | 官网与开源项目核验；中文学习价值明确，现有 ID、规范化网址及名称均未重复。 | [新入口](https://www.hello-algo.com/)；[来源 1](https://www.hello-algo.com/) |
| 现代 JavaScript 教程 | zh-javascript-info | 官网与开源项目核验；中文学习价值明确，现有 ID、规范化网址及名称均未重复。 | [新入口](https://zh.javascript.info/)；[来源 1](https://zh.javascript.info/) |

### 更新与迁移

| 条目 | ID | 原因 | 证据 / 新入口 |
| --- | --- | --- | --- |
| Carrd | carrd-co | 官方永久跳转及目标页面核验 | [新入口](https://carrd.com/)；[来源 1](https://carrd.co/)；[来源 2](https://carrd.com/) |
| ABC News | abcnews-go-com | 官方永久跳转及目标页面核验 | [新入口](https://abcnews.com/)；[来源 1](https://abcnews.go.com/)；[来源 2](https://abcnews.com/) |
| WorldCat | worldcat-org | 官方永久跳转及目标页面核验 | [新入口](https://search.worldcat.org/)；[来源 1](https://www.worldcat.org)；[来源 2](https://search.worldcat.org/) |
| Inciteful | inciteful-xyz | 官方永久跳转及目标页面核验 | [新入口](https://incitefulmed.com/academic/)；[来源 1](https://inciteful.xyz/)；[来源 2](https://incitefulmed.com/academic/) |
| Google Cloud Docs | cloud-google-com-docs | 官方永久跳转及目标页面核验 | [新入口](https://docs.cloud.google.com/docs)；[来源 1](https://cloud.google.com/docs)；[来源 2](https://docs.cloud.google.com/docs) |
| Elixir Docs | hexdocs-pm-elixir | 官方永久跳转及目标页面核验 | [新入口](https://elixir.hexdocs.pm/)；[来源 1](https://hexdocs.pm/elixir/)；[来源 2](https://elixir.hexdocs.pm/) |
| PyTorch Docs | pytorch-org-docs-stable-index-html | 官方永久跳转及目标页面核验 | [新入口](https://docs.pytorch.org/docs/stable/index.html)；[来源 1](https://pytorch.org/docs/stable/index.html)；[来源 2](https://docs.pytorch.org/docs/stable/index.html) |
| LangChain Docs | python-langchain-com-docs | 官方永久跳转及目标页面核验 | [新入口](https://docs.langchain.com/oss/python/langchain/overview)；[来源 1](https://python.langchain.com/docs/)；[来源 2](https://docs.langchain.com/oss/python/langchain/overview) |
| LlamaIndex Docs | docs-llamaindex-ai | 官方永久跳转及目标页面核验 | [新入口](https://developers.llamaindex.ai/python/framework/)；[来源 1](https://docs.llamaindex.ai/)；[来源 2](https://developers.llamaindex.ai/python/framework/) |
| Spotify for Podcasters | podcasters-spotify-com | 官方永久跳转及目标页面核验 | [新入口](https://creators.spotify.com/)；[来源 1](https://podcasters.spotify.com/)；[来源 2](https://creators.spotify.com/) |
| Megaphone | megaphone-fm | 官方永久跳转及目标页面核验 | [新入口](https://megaphone.spotify.com/)；[来源 1](https://www.megaphone.fm/)；[来源 2](https://megaphone.spotify.com/) |
| Nomad List | nomadlist-com | 官方永久跳转及目标页面核验 | [新入口](https://nomads.com/)；[来源 1](https://nomadlist.com/)；[来源 2](https://nomads.com/) |
| Threads | threads-net | 官方永久跳转及目标页面核验 | [新入口](https://www.threads.com/)；[来源 1](https://www.threads.net)；[来源 2](https://www.threads.com/) |
| Max | max-com | 官方永久跳转及目标页面核验 | [新入口](https://www.hbomax.com/)；[来源 1](https://www.max.com)；[来源 2](https://www.hbomax.com/) |
| DIRECTV Stream | streamtv-directv-com | 官方永久跳转及目标页面核验 | [新入口](https://www.directv.com/stream/)；[来源 1](https://streamtv.directv.com/)；[来源 2](https://www.directv.com/stream/) |
| Financial Modeling Prep | financialmodelingprep-com | 官方永久跳转及目标页面核验 | [新入口](https://site.financialmodelingprep.com/)；[来源 1](https://financialmodelingprep.com/)；[来源 2](https://site.financialmodelingprep.com/) |
| Mozilla Observatory | mozilla-observatory | 官方永久跳转及目标页面核验 | [新入口](https://developer.mozilla.org/en-US/observatory)；[来源 1](https://observatory.mozilla.org)；[来源 2](https://developer.mozilla.org/en-US/observatory) |
| Ente Auth | ente-io-auth | 官方永久跳转及目标页面核验 | [新入口](https://ente.com/auth/)；[来源 1](https://ente.io/auth/)；[来源 2](https://ente.com/auth/) |
| VeraCrypt | veracrypt-fr-en-home-html | 官方永久跳转及目标页面核验 | [新入口](https://veracrypt.io/en/Home.html)；[来源 1](https://www.veracrypt.fr/en/Home.html)；[来源 2](https://veracrypt.io/en/Home.html) |
| Rijksmuseum Collection | rijksmuseum-nl-en-rijksstudio | 官方永久跳转及目标页面核验 | [新入口](https://www.rijksmuseum.nl/en/collection)；[来源 1](https://www.rijksmuseum.nl/en/rijksstudio)；[来源 2](https://www.rijksmuseum.nl/en/collection) |
| 民报 | peoplemedia-tw | 官方永久跳转及目标页面核验 | [新入口](https://www.peoplenews.tw/)；[来源 1](https://www.peoplemedia.tw/)；[来源 2](https://www.peoplenews.tw/) |
| OldVersion | oldversion-com | 官方永久跳转及目标页面核验 | [新入口](https://www.oldversion.com/)；[来源 1](http://www.oldversion.com/)；[来源 2](https://www.oldversion.com/) |
| ExpressionEngine&#174; Answers | expressionengine-stackexchange-com | 修复名称中未解码的 HTML 字符实体。 | [来源 1](https://expressionengine.stackexchange.com) |
| Stack Overflow em Portugu&#234;s | pt-stackoverflow-com | 修复名称中未解码的 HTML 字符实体。 | [来源 1](https://pt.stackoverflow.com) |
| Stack Overflow en espa&#241;ol | es-stackoverflow-com | 修复名称中未解码的 HTML 字符实体。 | [来源 1](https://es.stackoverflow.com) |
| 芳斯塔芙 | funscience-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UClLEMac0ZjZCsVOTiaBtJBg)；[来源 1](https://www.youtube.com/@funstuff2018)；[来源 2](https://www.youtube.com/@FunScience) |
| 文森说书 | vincentbook-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UCPgGtH2PxZ9xR0ehzQ27FHw)；[来源 1](https://www.youtube.com/@vincent_reading)；[来源 2](https://www.youtube.com/@vincentbook) |
| 科技狗 3C Dog | techdog-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UC5r-9EMDERXlUni-UWAtTdg)；[来源 1](https://www.youtube.com/@3cdogs)；[来源 2](https://www.youtube.com/@TechDog) |
| X 调查 | x-investigations-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UCOyshL6rKK1GqwoEfy_ehBg)；[来源 1](https://www.youtube.com/@xdiaocha)；[来源 2](https://www.youtube.com/@XInvestigations) |
| 李自然说 | linvo-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UCgLUl1WDoDXUtxPaZeSZHsw)；[来源 1](https://www.youtube.com/@lzrshuo)；[来源 2](https://www.youtube.com/@Linvo) |
| Cheap | cheap-history-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UCGGrblndNzi86WY5lJkQJiA)；[来源 1](https://www.youtube.com/channel/UCGGrblndNzi86WY5lJkQJiA)；[来源 2](https://www.youtube.com/@CheapHistory) |
| 极客湾 Geekerwan | geekerwan-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UCeUJO1H3TEXu2syfAAPjYKQ)；[来源 1](https://www.youtube.com/@geekerwan1024)；[来源 2](https://www.youtube.com/@Geekerwan) |
| 点 Cook Guide | dimcookguide-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UCXnWjmQ8BDE0sDIeZLK5yJg)；[来源 1](https://www.youtube.com/user/dimcookguide)；[来源 2](https://www.youtube.com/@dimcookguide) |
| 笑波子 | smileboyhk-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UCDpK1rg5I9Zc3ToY13vbR3w)；[来源 1](https://www.youtube.com/@smilingboris1118)；[来源 2](https://www.youtube.com/@smileboyhk) |
| 大J | dajj-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UCJfKbbSaleFcT1Dg_b2Nepg)；[来源 1](https://www.youtube.com/@jstud1o)；[来源 2](https://www.youtube.com/@dajj) |
| 阿神 | asenstudio-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UCnJEWsS5agXCkqIpyHC9Grg)；[来源 1](https://www.youtube.com/channel/UCnJEWsS5agXCkqIpyHC9Grg)；[来源 2](https://www.youtube.com/@AsenStudio) |
| 米纸 | mill-milk-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UCGKZBiAkSYd1v1O_5vFky7A)；[来源 1](https://www.youtube.com/@ricezi2hk)；[来源 2](https://www.youtube.com/@MillMilk) |
| 毛记电视 | 100most-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UCiJnCs2K5gP-DXnMxlstC9A)；[来源 1](https://www.youtube.com/@100MOSTHongKong)；[来源 2](https://www.youtube.com/user/100mosthk) |
| 范琪斐的美国时间 | fan-america-time-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UC2VKL-DkRvXtWkfjMzkYvmw)；[来源 1](https://www.youtube.com/channel/UC2VKL-DkRvXtWkfjMzkYvmw)；[来源 2](https://www.youtube.com/@TheStormMedia) |
| 蔡阿嘎 | tsaigray-youtube | 纠正指向其他账号、子频道或错误语言版本的链接；用已核对名称与简介的稳定频道 ID。 | [新入口](https://www.youtube.com/channel/UCPwxSX0DYDMQxCvgfeVDv_g)；[来源 1](https://www.youtube.com/channel/UCPwxSX0DYDMQxCvgfeVDv_g)；[来源 2](https://www.youtube.com/@tsaigray2018) |
| 影视飓风 | mediastorm-youtube | 原链接指向另一 MediaStormfilm 账号；核对正确中文频道与资料页。 | [新入口](https://www.youtube.com/channel/UC2cRwTuSWxxEtrRnT4lrlQA)；[来源 1](https://www.youtube.com/channel/UC2cRwTuSWxxEtrRnT4lrlQA)；[来源 2](https://zh.wikipedia.org/wiki/影视飓风) |
| Marginalia Search | search-marginalia-nu | 官方跳转及目标内容确认当前入口；不采用地区、登录、实验参数或文档固定版本跳转。 | [新入口](https://marginalia-search.com/)；[来源 1](https://search.marginalia.nu)；[来源 2](https://marginalia-search.com/) |
| Library and Archives Canada | library-archives-canada-ca | 官方跳转及目标内容确认当前入口；不采用地区、登录、实验参数或文档固定版本跳转。 | [新入口](https://www.canada.ca/en/library-archives.html)；[来源 1](https://library-archives.canada.ca/)；[来源 2](https://www.canada.ca/en/library-archives.html) |
| Read the Docs | readthedocs-org | 官方跳转及目标内容确认当前入口；不采用地区、登录、实验参数或文档固定版本跳转。 | [新入口](https://about.readthedocs.com/)；[来源 1](https://readthedocs.org/)；[来源 2](https://about.readthedocs.com/) |
| GitLab | gitlab-com | 官方跳转及目标内容确认当前入口；不采用地区、登录、实验参数或文档固定版本跳转。 | [新入口](https://about.gitlab.com/)；[来源 1](https://gitlab.com)；[来源 2](https://about.gitlab.com/) |
| Remix Docs | remix-run-docs-en | 官方跳转及目标内容确认当前入口；不采用地区、登录、实验参数或文档固定版本跳转。 | [新入口](https://v2.remix.run/docs/)；[来源 1](https://remix.run/docs/en/main)；[来源 2](https://v2.remix.run/docs/) |
| age | age-encryption-org | 官方跳转及目标内容确认当前入口；不采用地区、登录、实验参数或文档固定版本跳转。 | [新入口](https://github.com/FiloSottile/age)；[来源 1](https://age-encryption.org/)；[来源 2](https://github.com/FiloSottile/age) |
| Laravel Docs | laravel-com-docs | 官方跳转及目标内容确认当前入口；不采用地区、登录、实验参数或文档固定版本跳转。 | [新入口](https://laravel.com/framework/docs)；[来源 1](https://laravel.com/docs)；[来源 2](https://laravel.com/framework/docs) |
| 一言堂 | yitianshijie-net | 核对当前官网品牌名称。 | [来源 1](https://yitianshijie.net/) |
| 镜传媒 | mirrormedia-mg | 核对当前官网品牌名称。 | [来源 1](https://www.mirrormedia.mg/) |
| 新头壳 Newtalk | newtalk-tw | 核对当前官网品牌名称。 | [来源 1](https://newtalk.tw/) |

### 归档

| 条目 | ID | 原因 | 证据 / 新入口 |
| --- | --- | --- | --- |
| Library of Congress | loc-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.loc.gov) |
| CIA World Factbook | cia-gov-the-world-factbook | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.cia.gov/the-world-factbook/) |
| MedlinePlus | medlineplus-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://medlineplus.gov/) |
| U.S. National Archives | archives-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.archives.gov/) |
| NASA | nasa-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.nasa.gov/) |
| NASA Images | images-nasa-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://images.nasa.gov/) |
| NOAA | noaa-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.noaa.gov/) |
| USGS | usgs-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.usgs.gov/) |
| USGS EarthExplorer | earthexplorer-usgs-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://earthexplorer.usgs.gov/) |
| PubMed | pubmed-ncbi-nlm-nih-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://pubmed.ncbi.nlm.nih.gov) |
| PubMed Central | pmc-ncbi-nlm-nih-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://pmc.ncbi.nlm.nih.gov/) |
| ERIC | eric-ed-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://eric.ed.gov/) |
| ClinicalTrials.gov | clinicaltrials-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://clinicaltrials.gov/) |
| CDC Publications | cdc-gov-library-researchguides | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.cdc.gov/library/researchguides/) |
| GenBank | ncbi-nlm-nih-gov-genbank | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.ncbi.nlm.nih.gov/genbank/) |
| PubChem | pubchem-ncbi-nlm-nih-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://pubchem.ncbi.nlm.nih.gov/) |
| SEC EDGAR | sec-gov-edgar-search | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.sec.gov/edgar/search) |
| Federal Reserve | federalreserve-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.federalreserve.gov/) |
| BLS | bls-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.bls.gov/) |
| BEA | bea-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.bea.gov/) |
| U.S. Treasury Data | fiscaldata-treasury-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://fiscaldata.treasury.gov/) |
| TreasuryDirect | treasurydirect-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.treasurydirect.gov/) |
| CDC Travelers' Health | cdc-gov-travel | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://wwwnc.cdc.gov/travel/) |
| CISA | cisa-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.cisa.gov) |
| NIST Cybersecurity | nist-cybersecurity | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.nist.gov/cybersecurity-and-privacy) |
| FTC IdentityTheft.gov | identitytheft-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.identitytheft.gov/) |
| FBI IC3 | ic3-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://www.ic3.gov/) |
| NVD | nvd-nist-gov | 美国联邦政府机构运营的公开资源，按仓库内容政策排除；不是恶意或失效判定。 | [来源 1](https://nvd.nist.gov/) |
| Proton VPN | protonvpn-com | VPN 服务，命中明确排除规则。 | [来源 1](https://protonvpn.com/) |
| Mullvad VPN | mullvad-net | VPN 服务，命中明确排除规则。 | [来源 1](https://mullvad.net/) |
| IVPN | ivpn-net | VPN 服务，命中明确排除规则。 | [来源 1](https://www.ivpn.net/) |
| Mozilla VPN | mozilla-org-products-vpn | VPN 服务，命中明确排除规则。 | [来源 1](https://www.mozilla.org/products/vpn/) |
| Tor Project | torproject-org | Tor/Tails 官方资助页明确列出美国国务院与 OTF 支持，按资金背景规则排除。 | [来源 1](https://www.torproject.org/about/supporters/) |
| Tor Metrics | metrics-torproject-org | Tor/Tails 官方资助页明确列出美国国务院与 OTF 支持，按资金背景规则排除。 | [来源 1](https://www.torproject.org/about/supporters/) |
| Tails | tails-net | Tor/Tails 官方资助页明确列出美国国务院与 OTF 支持，按资金背景规则排除。 | [来源 1](https://www.torproject.org/about/supporters/) |
| Smithsonian | si-edu | 机构披露美国联邦拨款；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://www.si.edu/about/reports) |
| Smithsonian Open Access | si-edu-openaccess | 机构披露美国联邦拨款；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://www.si.edu/about/reports) |
| PhysioNet | physionet-org | 项目披露 NIH 资助；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://physionet.org/about/) |
| OpenNeuro | openneuro-org | 项目披露 NIMH/NIH R24 资助；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://docs.openneuro.org/policy/data_management_plans.html) |
| Protein Data Bank | rcsb-org | 项目披露 NSF、DOE 和 NIH 资助；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://cdn.rcsb.org/rcsb-pdb/general_information/news_publications/newsletters/2026q3/statement.html) |
| UniProt | uniprot-org | 运营方披露 NIH 主要资助；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://www.ebi.ac.uk/training/online/courses/uniprot-quick-tour/get-help-and-support-on-uniprot/) |
| NASA ADS | ui-adsabs-harvard-edu | 项目披露 NASA 合作协议资助；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://prod.adsabs.harvard.edu/about/) |
| arXiv | arxiv-org | arXiv 年报披露 500 万美元 NSF 项目拨款，ar5iv 为其托管的实验资源；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://info.dev.arxiv.org/about/reports/2023_arXiv_annual_report.pdf) |
| ar5iv | ar5iv-labs-arxiv-org | arXiv 年报披露 500 万美元 NSF 项目拨款，ar5iv 为其托管的实验资源；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://info.dev.arxiv.org/about/reports/2023_arXiv_annual_report.pdf) |
| CVE | cve-org | 项目披露 CISA 资助；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://www.cve.org/Resources/Media/Archives/OldWebsite/community/sponsor.html) |
| MITRE ATT&CK | attack-mitre-org | 运营方 MITRE 披露美国联邦资助研究中心背景；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://www.mitre.org/who-we-are/our-story) |
| CERT/CC | kb-cert-org | CERT/CC 隶属服务美国国防部门的 SEI 联邦资助研究中心；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://www.sei.cmu.edu/about/) |
| Freedom House | freedomhouse-org | 2025 审计披露 91% 收入来自美国政府拨款；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://freedomhouse.org/sites/default/files/2026-01/FH%202025%20Final%20Financial%20Statements%20and%20Audit%27s%20Report.pdf) |
| Qubes OS | qubes-os-org | 官方历史合作伙伴页披露美国政府资助的 OTF 支持；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://www.qubes-os.org/partners/) |
| SecureDrop | securedrop-org | 2024 安全审计明确由 OTF 出资；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://www.opentech.fund/wp-content/uploads/2024/10/SEC-01-SecureDrop-Audit-Report_PublicRC1.3.pdf) |
| NBER | nber-org | 官方资金支持页列出 NIH 与 NSF 资助；按仓库资金背景排除规则归档，不作安全性负面判断。 | [来源 1](https://www.nber.org/support-funding) |
| 文昭谈古论今 | wenzhao-youtube | 公开作者页与节目转载记录显示与仓库排除的传播网络存在持续内容合作；按仓库传播网络规则排除。 | [来源 1](https://www.epochtimes.com/gb/authors/%E6%96%87%E6%98%AD.html)；[来源 2](https://www.ntdtv.com/gb/author/prog1122) |
| GetMacApps | getmacapps-com | 原 Mac 应用工具入口现已变为无身份验证赌场推荐与博彩联盟推广页；普通 GET 两次核验。 | [来源 1](https://www.getmacapps.com/) |
| 精选副业 | jingxuan-fuye-pages-dev | 页面无公开案例，主要引导领取体验卡及专属邀请链接加入付费社群；命中联盟营销空壳页排除规则。 | [来源 1](https://jingxuan-fuye.pages.dev/) |
| Poker | poker-stackexchange-com | 扑克下注与策略问答社区，命中赌博及下注推荐方向排除规则。 | [来源 1](https://poker.stackexchange.com/tour) |
| Typepad | typepad-com | 运营方公告服务于 2025-09-30 终止；不因本轮 403 单独判失效。 | [来源 1](https://www.networksolutions.com/typepad) |
| Read.cv | read-cv | 已宣布关停；本轮仅返回 DEPLOYMENT_DISABLED。 | [来源 1](https://www.neowin.net/news/readcv-announces-acquisition-by-perplexity-as-it-begins-winding-down-operations/) |
| DNS0.eu | dns0-eu | 域名无法解析，并有独立停服报道。 | [来源 1](https://www.bleepingcomputer.com/news/security/dns0eu-private-dns-service-shuts-down-over-sustainability-issues/) |
| Nebula Classes | classes-nebula-tv | 原课程子域名两次无法解析；Cloudflare 与 Google 独立 DNS 查询均无 A/AAAA 记录，归档失效子入口，保留 Nebula 主站。 | [来源 1](https://classes.nebula.tv/) |
| JustPod | justpodmedia-com | 公开目录现用 justpod.com 两次返回明确 404；原域名也无法正常完成 TLS。节目仍更新，不将机构认定为停业。 | [来源 1](https://www.justpod.com/)；[来源 2](https://www.xiaoyuzhoufm.com/podcast/5e4ee557418a84a0466737b7) |
| KKTV | kktv-me | 同步此前已有的停服排除决定至数据库及静态主站：KKTV official notices state service ended on 2026-01-01. | [来源 1](https://events.kktv.me/tw/announcement-165) |
| 澳洲新快网 | xkb-com-au | 同步此前已有的停服排除决定至数据库及静态主站：Australian New Express Daily website is unavailable and public sources indicate the website stopped updating from 2021-04-01. | [来源 1](https://www.sbs.com.au/language/chinese/zh-hans/article/australian-new-express-daily-ceased-publication/5zf6mdtrs) |
| OpenStax CNX | cnx-org | 旧入口永久跳转至已收录的 OpenStax，合并重复入口。 | [来源 1](https://cnx.org/)；[来源 2](https://openstax.org/) |
| Warpcast | warpcast-com | Warpcast 永久跳转至已收录的 Farcaster，合并重复入口。 | [来源 1](https://warpcast.com/)；[来源 2](https://farcaster.xyz/) |
| Papers with Code | paperswithcode-com | 原站跳转至已收录的 Hugging Face Papers，原独立服务入口不再可用。 | [来源 1](https://paperswithcode.com/)；[来源 2](https://huggingface.co/papers/trending) |
| Flathub Apps | flathub-org-apps | 应用入口永久跳转至与已收录 Flathub 首页相同的位置，合并重复入口。 | [来源 1](https://flathub.org/apps)；[来源 2](https://flathub.org/en) |
| 罗翔说刑法 | luoxiang-youtube | 现有 @luoxiang 实际为 XIANG，内容与罗翔说刑法不符；未确认官方替代频道，不以同名搜索结果替换。 | [来源 1](https://www.youtube.com/@luoxiang) |
| cppreference | en-cppreference-com-w | 旧 /w/ 入口永久跳转至已经收录的 cppreference 首页，合并重复入口。 | [来源 1](https://en.cppreference.com/w/)；[来源 2](https://en.cppreference.com/) |
