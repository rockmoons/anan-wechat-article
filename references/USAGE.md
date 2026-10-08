# 用法速查（anan-wechat-article）

脚本：`scripts/wechat_spider.py`　命令在**技能根目录**执行。

## 1. 三条最常用的命令

```bash
# ① 抓一篇
python scripts/wechat_spider.py "https://mp.weixin.qq.com/s/h0IthL_gWPmyT8kMbc537w"

# ② 批量抓（每行一个链接，--delay 限速，建议 >= 5 秒）
python scripts/wechat_spider.py --urls-file urls.txt --delay 5

# ③ 只抓文字，不要图片
python scripts/wechat_spider.py "https://mp.weixin.qq.com/s/h0IthL_gWPmyT8kMbc537w" --no-images
```

## 2. 常用变体

| 需求 | 命令 |
| --- | --- |
| 指定输出目录 | `python scripts/wechat_spider.py "<url>" -o D:\素材\公众号` |
| 慢速批量（更稳） | `python scripts/wechat_spider.py --urls-file urls.txt --delay 8 --img-delay 1` |
| 单独一篇 + 不要图片 | `python scripts/wechat_spider.py "<url>" --no-images -o output_text` |
| 网络慢，放宽超时 | `python scripts/wechat_spider.py "<url>" --timeout 60` |
| 看全部参数 | `python scripts/wechat_spider.py --help` |

## 3. 链接清单文件（urls.txt）格式

```text
# 以 # 开头的是注释，空行会被忽略
https://mp.weixin.qq.com/s/h0IthL_gWPmyT8kMbc537w
https://mp.weixin.qq.com/s/aaaaaaaaaaaaaaaa
```

文件用 UTF-8 保存。可以同时给位置参数和 `--urls-file`，两者会合并。

## 4. 参数默认值

| 参数 | 默认 | 备注 |
| --- | --- | --- |
| `--outdir` / `-o` | `output` | 相对**当前工作目录**，不是脚本所在目录 |
| `--delay` | 3.0 | 文章之间；批量建议 ≥ 5 |
| `--img-delay` | 0.5 | 图片之间 |
| `--timeout` | 30 | 秒 |
| `--no-images` | 关 | 不建 `images/` 目录 |
| `--allow-any-url` | 关 | 跳过域名校验，不建议 |

## 5. 输出目录长什么样

```text
output/
├── <文章标题>/
│   ├── <文章标题>.md      正文（图片为本地相对路径）
│   ├── images/01.png ...  正文图片
│   ├── cover.jpg          封面图
│   ├── 文章信息.md / .csv 该文章信息 + 图片清单
│   └── meta.json          结构化信息
├── 文章信息表.csv          汇总表（Excel 可直接打开）
└── 文章信息表.md           汇总表（Markdown）
```

命名细节：

- 文件夹与 Markdown 文件名 = 文章标题，非法字符换成 `_`，超长截断到 60 字。
- 标题抓不到时，用 `文章_<链接短标识>` 兜底。
- 图片按正文出现顺序编号：`01.png`、`02.jpg`……扩展名按服务器返回的真实类型。
- 汇总表按「原文链接」去重，同一篇重复跑会覆盖旧记录，不会重复记账。

## 6. 推荐工作流（抓下来之后接着做加工）

1. **先抓**到独立目录：`-o <工作目录>/素材`，跟其他文件分开。
2. **读** `<文章标题>/<文章标题>.md` 做分析、拆解、改写、提炼。
3. **图片**直接用 `images/` 里的本地文件，不用再联网。
4. 汇总表可用于统计「一共抓了多少篇、都是哪些号」。

## 7. 命令行注意事项

- **链接一定要加引号**：公众号链接常含 `&`（`?__biz=...&mid=...`），不加引号会被 shell 截断。
- PowerShell 下用双引号最稳：`"https://mp.weixin.qq.com/s/xxxx?__biz=xx&mid=xx"`
- 路径含中文没问题；Windows 上建议用 Python 3.8+ 的官方解释器。
- 建议一次只跑一个实例；并发跑容易触发微信风控。

## 8. 合规提醒

抓来的内容是**自用素材**。**原样搬运别人的文章发布 = 侵权**；引用要注明出处 + 原文链接，转载/商用要授权。
