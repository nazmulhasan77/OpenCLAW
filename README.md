# OpenCLAW
**Complete OpenClaw installation, configuration, and uninstallation guide for MacOS** in **English**. I’ll make it step-by-step so nothing is missed.

---

# 1️⃣ Prerequisites

To run **OpenClaw** on Mac, you need:

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

# 2️⃣ Installing OpenClaw

### a) Update Node.js (if needed)

If you have **nvm**:

```bash
nvm install 22
nvm use 22
nvm alias default 22
```

---

### b) Install OpenClaw

```bash
npm install -g openclaw
```

or with pnpm:

```bash
pnpm add -g openclaw
```

✅ Verify installation:

```bash
openclaw --version
```

* Output example: `OpenClaw 2026.3.8`

---

# 3️⃣ Configuring OpenClaw

1️⃣ **Initialize default config:**

```bash
openclaw init
```

2️⃣ **Add API key** (if using OpenAI models):

```bash
openclaw config set openai.api_key YOUR_API_KEY
```

3️⃣ **Set local AI model** (optional):

```bash
openclaw model set gpt-5.1-codex
```

4️⃣ **Add / enable skills**:

```bash
openclaw skill add file
openclaw skill add terminal
openclaw skill add git
```

5️⃣ **Run a test**:

```bash
openclaw run
```

* This will start the agent and show logs in the terminal.

---

# 4️⃣ Uninstalling OpenClaw

### a) Remove from npm / pnpm

```bash
npm uninstall -g openclaw
```

or

```bash
pnpm remove -g openclaw
```

---

### b) Delete configuration / cache

```bash
rm -rf ~/.openclaw
rm -rf ~/.cache/openclaw
```

---

### c) Verify

```bash
openclaw --version
```

* Output: `command not found` → OpenClaw is fully removed

---