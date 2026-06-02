# Dont-Be-Stupid-Leaker

<p align="center">
  <a href="https://github.com/cdfd426-beep/Dont-Be-Stupid-Leaker">
    <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=32&pause=1000&color=FF4444&center=true&vCenter=true&width=500&lines=LLMApiCheckBot;%E5%88%AB%E5%BD%93%E5%82%BB%E9%80%BC%E6%B3%84%E9%9C%B2%E8%80%85"/>
  </a>
</p>

---

![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/cdfd426-beep/Dont-Be-Stupid-Leaker/scan.yml)
![GitHub Issues](https://img.shields.io/github/issues/cdfd426-beep/Dont-Be-Stupid-Leaker)
![GitHub last commit](https://img.shields.io/github/last-commit/cdfd426-beep/Dont-Be-Stupid-Leaker)

## 这是什么 / What is This

```
ENG: A GitHub Actions bot that scans commits and issues for leaked API keys,
     then replies with a ~~rude~~ polite warning.
     
ZH : 一个 GitHub Actions 机器人，扫描 commits 和 issues 里泄露的 API Key，
     然后回复一条~~阴阳怪气~~友好的提醒。
```

## 检测的格式 / Detected patterns

· `sk-proj-*` / `sk-*` (OpenAI, DeepSeek, GLM)
· `sk-or-v1-*` (OpenRouter)
· `AIza*` (Gemini)
· `sk-ant-api*` (Anthropic)
· `tp-*` (MiMo)
· `r8_*` (Replicate)
· `hf_*` (HuggingFace)

## 工作原理 / How It Works

```yaml
Schedule:
  - cron: '0 * * * *'  # every hour / 每小时

Workflow:
  1. Search recent commits with key patterns
  2. Search recent issues with "your key leak"
  3. Verify each key via provider API
  4. If valid -> reply with warning
  5. Save state -> never reply twice
```

## 部署步骤 / Deployment Steps

### 中文

1. ✅ 已完成：已复制 `.github/workflows/scan.yml` 和 `.github/scripts/scan_keys.py` 到仓库
2. ⚠️ **需要在 GitHub Secrets 中配置以下环境变量**：

   前往仓库的 **Settings → Secrets and variables → Actions**，添加以下 secret：

   - `APP_ID` - GitHub App ID
   - `PRIVATE_KEY` - GitHub App Private Key（PEM 格式）
   - `INSTALLATION_ID` - GitHub App Installation ID  
   - `PAT_TOKEN` - 个人访问令牌（用于在发现的泄露处回复）

3. 🔧 **推荐方式**：使用小号创建 GitHub App 来获取认证信息
4. ⏱️ 推送后，机器人每小时自动运行

### English

1. ✅ Done: Copied `.github/workflows/scan.yml` and `.github/scripts/scan_keys.py` to repo
2. ⚠️ **Configure the following environment variables in GitHub Secrets**:

   Go to **Settings → Secrets and variables → Actions** and add these secrets:

   - `APP_ID` - GitHub App ID
   - `PRIVATE_KEY` - GitHub App Private Key (PEM format)
   - `INSTALLATION_ID` - GitHub App Installation ID  
   - `PAT_TOKEN` - Personal Access Token (for replying to discovered leaks)

3. 🔧 **Recommended**: Create a GitHub App using a secondary account
4. ⏱️ After push, bot runs automatically every hour

## 示例回复 / Example Reply

```
@someone Your API key has been exposed in a commit!

# Summary
This is a **DeepSeek** API key in commit [abc1234](https://github.com/...).

Location: code diff (line 42)
Key preview: `sk-abc123...xyz789`

Verification result: Balance: CNY 6.66, USD 0.00

---

**What to do:**
1. Revoke this key from DeepSeek dashboard
2. Generate a new key
3. Remove from git history using BFG Repo Cleaner
4. Rotate other exposed secrets

**Exposed code:**
`Authorization: Bearer sk-abc123def456...`

---
*This message was sent by LLMApiCheckBot - Repository: Dont-Be-Stupid-Leaker*
```

## 免责声明 / Disclaimer

```
ENG: This bot is for educational purposes only.
     Don't leak API keys. Use environment variables.
     If you get roasted by this bot, that's a skill issue.

ZH : 本机器人仅供学习交流。
     别泄露 API Key，用环境变量。
     如果你被这个机器人嘲讽了，那是你菜。
```

---

Made with 💀 and ☕