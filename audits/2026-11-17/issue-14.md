# Issue #14 收录核验

- 日期：2026-11-17。
- 请求：[运动营养健康指南 #14](https://github.com/ifanqiang-com/chinese-open-web-directory/issues/14)。
- 官网：<https://jiangweiqi001.github.io/sports-nutrition-health/search.html>。
- 公开源码：<https://github.com/jiangweiqi001/sports-nutrition-health>。

## 适合性与链接

2026-11-16 初审确认中文检索页公开可访问，无需登录；可按章节与编辑证据分级检索运动、营养和健康问答，抽查条目标注适用范围与参考出处。未发现触发本次收录排除规则的具体证据。项目仍较新，收录不构成对所有医学内容的认证；简介明确提示内容不能替代专业诊疗。

提交者已在[原 Issue 留言](https://github.com/ifanqiang-com/chinese-open-web-directory/issues/14#issuecomment-6921266411)，提供了[友情链接页面](https://jiangweiqi001.github.io/sports-nutrition-health/search.html#friend-links)。本次实际打开页面，确认页脚公开显示可点击的 ifanqiang.com 链接；点击后导航至 `https://ifanqiang.com/`。源代码变更亦可核对：[添加页脚链接的提交](https://github.com/jiangweiqi001/sports-nutrition-health/commit/ef4d91ef0aca292ac02d3c55801f2bc190d4604b)。本次跟进不重复索要链接。

## 数据变更与检查

- 生产目录数据源中无相同 ID、站名或网站地址记录；事务仅新增 `sports-nutrition-health`，分类为“百科与开放资料”。未更改其他网站或频道记录。
- 导出后公开网站由 1436 增至 1437，YouTube 频道仍为 67。
- 同步静态主站同一条目，三方逐字段校验一致。
- 修正本条目的专题误匹配：`search.html` 包含 `Arch` 子串，Linux 文档分组排除“运动训练”标签，避免将此健康资源列为系统文档。其他已生成专题条目保持不变。
- 执行目录导出与 schema 校验、主站类型检查及本地静态构建；同时运行主站要求的加密目录回归测试和提交内容检查，不改动其数据或密钥。
- 使用独立工作树与 PR；未覆盖用户未提交改动，未执行生产静态站部署。
