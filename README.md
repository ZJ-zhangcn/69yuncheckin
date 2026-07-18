# 69 云签到

GitHub Actions 定时签到，可选 Telegram 通知。

| 项 | 值 |
|---|---|
| 仓库 | https://github.com/ZJ-zhangcn/69yuncheckin |
| 上游 | https://github.com/yixiu001/69yuncheckin |

## 配置

仓库 **Settings → Secrets and variables → Actions** 添加：

| Secret | 含义 |
|---|---|
| `BOT_TOKEN` | Telegram Bot Token |
| `CHAT_ID` | Telegram Chat ID |
| `USER1` / `PASS1` | 账号 1 |
| `USER2` / `PASS2` | 账号 2（可选） |
| `USER3` / `PASS3` | 账号 3（可选） |

> workflow 默认账户数有限；多于 2 个时需改 `.github/workflows` 里的 yaml。

## 运行

- 自动：按 workflow 的 `schedule` / `push` 触发  
- 手动：Actions 页 **Run workflow**

不要把账号密码写进代码或 README。
