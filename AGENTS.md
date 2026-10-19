# AGENTS.md — csnote

个人技术笔记仓库（GitHub: https://github.com/godjupit/csnote ）。笔记用 Markdown 按主题放在子目录里（如 `infra/`），图片与笔记同目录、用相对路径引用。

## 一、改完笔记后：自动提交并推送

不要询问，直接执行：

```bash
git add -A
git commit -m "<信息>"
git push origin main
```

- commit message 用日期或一句话说明，风格参考历史提交（如 `9/26`、`10.5`）。
- `.DS_Store` 已被 `.gitignore` 忽略，不要提交系统文件。
- 推送失败时先 `git pull --rebase origin main` 再推；永远不要 force push。
- 连不上 github.com 时（网络受限），临时走本机代理推送：`git -c http.proxy=http://127.0.0.1:7897 -c https.proxy=http://127.0.0.1:7897 push origin main`（博客仓库同理）。

## 二、然后：同步到 GitHub 博客

博客仓库（本地已存在）：

```
/Users/wangqibo/cs3.1/parallel-computing/godjupit.github.io
```

线上地址 https://godjupit.github.io/ ，GitHub Pages 从 `main` 分支根目录自动发布。本地副本缺失时先克隆：

```bash
git clone https://github.com/godjupit/godjupit.github.io.git /Users/wangqibo/cs3.1/parallel-computing/godjupit.github.io
```

同步规则——一篇笔记对应一篇文章：

1. **新增了一个 md 笔记** → 在博客 `notes/` 下新建一篇文章页，并在 `index.html` 的文章列表加一张卡片、更新文章数量。
2. **修改了已有 md 笔记** → 更新它对应的文章页，不新建页面。
3. **空笔记、草稿、已删除的笔记** → 不发布；曾发布过的要把文章页和首页卡片一起删掉。
4. 文章用中文整理，保留学习记录的措辞；页面结构、主题切换和样式沿用现有文章页（参考 `notes/cuda-memory.html`，正文用 `detail-*` 类）。

当前映射：

| 笔记 | 文章 |
| --- | --- |
| `infra/cuda.md` | `notes/cuda-memory.html` |
| `infra/mpi.md` | 尚未发布（文件为空） |
| `database/sql_practice.md` | `notes/sql-practice.html` |

新增文章后，在这里补一行映射。

博客改动同样提交推送：

```bash
cd /Users/wangqibo/cs3.1/parallel-computing/godjupit.github.io
git add -A && git commit -m "<信息>" && git push origin main
```

推送后验证页面可访问：

```bash
curl -s -o /dev/null -w '%{http_code}\n' https://godjupit.github.io/
curl -s -o /dev/null -w '%{http_code}\n' https://godjupit.github.io/notes/<文章>.html
```

## 三、注意

- 不要发布隐私、密钥、个人信息或未经确认的第三方图片（如课件截图）。
- 不要 force push，不要重写已推送的历史。
- 笔记里不确定的内容，整理成文章时保留“整理中”的说法，不要编造结论。
