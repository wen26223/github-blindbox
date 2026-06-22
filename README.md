# GitHub 每日盲盒

**每天 18:00，AI 自动从 GitHub Trending 筛选真正值得关注的项目，按「创意好玩 / 工具 / AI 应用」三类整理好，发到你 QQ 邮箱。**

如果你刷 GitHub Trending 感觉噪音太多——每天几十个项目，大部分是底层技术库、算法、框架——那这个工具就是为你准备的。AI 帮你过滤，只留下对独立开发者 / 产品思维的人有用的内容。

---

## 怎么用（2 分钟上手）

读完我的介绍，把 [`AI-GUIDE.md`](AI-GUIDE.md) 丢给你的 AI 编程助手（Trae / Cursor / Windsurf 等），跟着引导走完 8 步即可。

**你需要自己准备的：**

| 需要准备 | 费用 | 时间 |
|---------|------|------|
| DeepSeek API Key | 1 元起充（最低充值） | 3 分钟 |
| QQ 邮箱授权码 | 免费 | 2 分钟 |
| GitHub 账号 + gh CLI | 免费 | 5 分钟 |

**AI 会自动帮你搞定：** 建仓库、下载代码、配置 Secrets、提交推送、触发测试。你只需要看着就行。

---

## 原理

```
我的仓库（数据源）                      球友的仓库
─────────────────                     ─────────────────
GitHub Actions 每天 05:00 抓取          你自己的 workflow
    ↓                                      ↓
commit trending-feed.json              curl 我的 raw 数据
    ↓                                      ↓
                                     AI 筛选 + 发邮件到 QQ 邮箱
```

- 抓取是我干的，你只需要配 AI + 邮箱
- 全部跑在 GitHub Actions 上，零成本
- 不需要服务器，不需要海外服务

## 常见问题

**Q：每天能收到多少项目？**
A：AI 从 50-80 个候选项目中筛选，最终推送 6-9 个（经典 2 个 + 新星 6-7 个）。

**Q：收不到邮件怎么办？**
A：检查 Secrets 是否正确，特别是 `QQ_SMTP_AUTH_CODE` 是不是 16 位授权码。手动 Run workflow 看报错日志最快。

**Q：可以用其他模型吗？**
A：可以。支持任何 OpenAI 兼容接口，改 `ANTHROPIC_BASE_URL` 和 `ANTHROPIC_MODEL` 两个 Secret 即可。

**Q：为什么必须 07:00 之后推送？**
A：我每天 05:00 抓取 commit，GitHub Actions 有队列延迟，07:00 之后确保数据已更新。
