# 🦞 OpenClaw Setup Guide for macOS

**Complete installation, configuration, and uninstallation instructions for OpenClaw on macOS.**
Includes running **local Ollama models**, pairing Telegram, and handling offline setups.

---

## 1️⃣ Prerequisites

Before installing OpenClaw:

* **Node.js 22+** (v20 won’t work)
* **npm / pnpm / yarn** (package manager)
* **Python 3.11+** (for some skills)
* Terminal access

Check versions:

```bash
node -v
npm -v
python3 --version
```

---

## 2️⃣ Installing OpenClaw

### a) Update Node.js (if needed)

If using **nvm**:

```bash
nvm install 22
nvm use 22
nvm alias default 22
```

### b) Install OpenClaw globally

```bash
npm install -g openclaw
# or
pnpm add -g openclaw
```

Verify installation:

```bash
openclaw --version
# Example: OpenClaw 2026.3.8
```

---

## 3️⃣ Initializing OpenClaw

Start onboarding (sets default config):

```bash
openclaw onboard
```

Open the dashboard:

```bash
openclaw dashboard
```

---

## 4️⃣ Configuring OpenClaw

### a) API Key (Optional — for OpenAI models)

```bash
openclaw config set openai.api_key YOUR_API_KEY
```

### b) Local Ollama model (offline)

1. **Start Ollama local server**:

```bash
ollama serve
```

2. **Create auth profile for Ollama**:

```bash
openclaw agents add ollama
# Provider: ollama
# API key: ollama-local
```

3. **Set primary model**:

```bash
openclaw config set agents.defaults.model.primary ollama/llama3:latest
# Disable tools for offline model
openclaw config set agents.defaults.model.disableTools true
```

4. **Restart gateway**:

```bash
openclaw gateway restart
```

5. **Start agent**:

```bash
openclaw agent start
```

> ✅ Now your OpenClaw agent uses a local Ollama model fully offline.

---

### c) Adding skills

Example skills:

```bash
openclaw skill add file
openclaw skill add terminal
openclaw skill add git
```

---

### d) Pair Telegram (Optional)

```bash
openclaw pairing approve telegram <PAIRING_CODE>
```

---

## 5️⃣ Verifying status

```bash
openclaw status
openclaw models status
```

* Check gateway, agent sessions, and channels.
* Make sure Ollama provider is **ready** and tokens are sufficient for your model.

---

## 6️⃣ Troubleshooting common issues

| Issue                                          | Solution                                                                           |
| ---------------------------------------------- | ---------------------------------------------------------------------------------- |
| **Model context too small**                    | Use a 16k token model (`llama3:16k-latest`) or fallback to OpenAI.                 |
| **No API key for Ollama**                      | Add auth profile: `openclaw agents add ollama` with key `ollama-local`.            |
| **Ollama API error 400 / tools not supported** | Disable tools: `openclaw config set agents.defaults.model.disableTools true`.      |
| **Agent fails to reply**                       | Restart gateway: `openclaw gateway restart`. Check logs: `openclaw logs --follow`. |

---

## 7️⃣ Uninstalling OpenClaw

### a) Stop gateway

```bash
openclaw gateway stop
```

### b) Remove global package

```bash
npm uninstall -g openclaw
# or
pnpm remove -g openclaw
```

### c) Delete workspace/configs

```bash
rm -rf ~/.openclaw
rm -rf ~/.cache/openclaw
```

### d) Verify removal

```bash
openclaw --version
# Output: command not found
```

---

## 8️⃣ Tips

* For **fully offline use**, stick to Ollama local models and disable tools.
* For **tool-enabled AI**, use online models or OpenAI fallback.
* Always restart gateway after changing model or auth settings.
* Use `openclaw status --deep` for detailed debugging.

---