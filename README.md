# anan-wechat-article · 阿南 · 微信公众号文章抓取

> 给「豆包工作」用的技能包：**给一个公众号文章链接，落成一份可离线归档的资料包。**

## 它能干什么

给一个 `mp.weixin.qq.com` 链接，它会把这篇东西抓下来，落成本地文件：

```
文章目录/
  正文.md            正文 Markdown
  图片/              原始图片（按顺序命名）
  封面图
  文章信息.md        标题 / 作者 / 发布时间 / 链接…
  文章信息.csv
  meta.json          给程序读的结构化信息
```

**并且自动维护一张跨文章的汇总总表** —— 抓得越多，总表越全。

## 安装

1. 下载本仓库（或用 Releases 里的 zip）
2. 在**豆包工作**里：市场 → 管理 → 上传技能 → 选择包含 `SKILL.md` 的文件夹/压缩包

> ⚠️ 上传的压缩包/文件夹必须**直接包含 `SKILL.md`**（不要多套一层文件夹）。

## 怎么用

```
把这个链接抓下来：https://mp.weixin.qq.com/s/xxxxx
```

或者直接**把链接丢给它**就行。

## 特点

- **零第三方依赖**：纯 Python 标准库，不需要 `pip install`
- **不需要任何密钥**：抓取走公开页面，不涉及公众号接口
- **离线可归档**：抓下来之后断网也能看

## 说明

- 只抓**你有权访问**的公开内容；请遵守对方版权与平台规则
- 抓不到阅读量 / 点赞数 —— 那些数字是登录后由 JS 异步填的，静态页面里是空的

## 环境

Python 3.8+（只用标准库）。Windows / macOS / Linux 均可。

## 授权

个人学习免费；**企业商用需先获得作者授权**（微信：rockmoons）。完整条款见 [LICENSE](LICENSE)。

Copyright (c) 2026 阿南 rockmoons

## 主要文件

- [`SKILL.md`](SKILL.md) —— 技能定义（给 AI 看的说明书）
- [`references/USAGE.md`](references/USAGE.md) —— 用法
- [`references/TROUBLESHOOTING.md`](references/TROUBLESHOOTING.md) —— 常见问题
- [`scripts/wechat_spider.py`](scripts/wechat_spider.py) —— 抓取脚本