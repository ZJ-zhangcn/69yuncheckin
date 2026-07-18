# 69 云签到

用 **GitHub Actions** 定时执行签到脚本，结果可通过 Telegram Bot 通知。  
Fork 自 [`yixiu001/69yuncheckin`](https://github.com/yixiu001/69yuncheckin)。

| 项 | 值 |
|---|---|
| 仓库 | https://github.com/ZJ-zhangcn/69yuncheckin |
| 分支 | `main` |
| 上游 | https://github.com/yixiu001/69yuncheckin |
| 与上游代码 | **基本同步上游脚本**；本 fork 侧重中文操作说明 |

## 与上游的区别

| 项 | 说明 |
|---|---|
| 签到逻辑 | 与上游同一套 `69yun.py` + workflow 思路 |
| 文档 | 可操作中文步骤（Secrets / 触发方式 / 多账号注意） |
| 功能分叉 | 无独立业务改动；要修脚本优先对照上游 |

## 部署方式（GitHub Actions）

本项目 **不需要 VPS**。部署 = Fork + 配 Secrets + 让 Actions 跑起来。

### 1. 使用本仓库或再 Fork 到你的账号

确保 Actions 已启用。

### 2. 配置 Secrets

路径：**Settings → Secrets and variables → Actions → New repository secret**

| Secret | 必填 | 含义 |
|---|---|---|
| `BOT_TOKEN` | 建议 | Telegram Bot Token |
| `CHAT_ID` | 建议 | Telegram Chat ID |
| `USER1` | 是 | 账号 1 用户名（如邮箱） |
| `PASS1` | 是 | 账号 1 密码 |
| `USER2` / `PASS2` | 否 | 账号 2 |
| `USER3` / `PASS3` | 否 | 账号 3 |

> workflow 文件里默认只声明了部分账户；超过已写变量时，需要编辑 `.github/workflows/69yuncheckin.yaml` 增加 `USER/PASS` 与脚本侧读取逻辑。

**不要**把账号密码写进代码或 README。

### 3. 触发方式

当前 workflow（见 `.github/workflows/69yuncheckin.yaml`）：

| 触发 | 说明 |
|---|---|
| `schedule` | `cron: '1 0 * * *'`（UTC 每天 0:01，折合其它时区自行换算） |
| `workflow_dispatch` | Actions 页手动 **Run workflow** |
| `push` → `main` | 推送主分支时也会跑（注意别误触） |

### 4. 手动跑一次验证

1. 打开 **Actions**  
2. 选中签到 workflow → **Run workflow**  
3. 看日志是否登录/签到成功；Telegram 是否收到通知  

## 本地调试（可选）

```bash
git clone https://github.com/ZJ-zhangcn/69yuncheckin.git
cd 69yuncheckin
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
export USER1=... PASS1=... BOT_TOKEN=... CHAT_ID=...
python 69yun.py
```

## 维护

- 上游脚本变更：`git fetch upstream && git merge upstream/main`  
- 仅改 Secrets 一般不必改代码  
