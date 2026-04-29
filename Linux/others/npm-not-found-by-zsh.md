# Fixing `npm: command not found` after switching from Bash to Zsh

⬅️ [Others](../others.md)

## 📌 Context

- Switched default shell from **bash → zsh**
- Installed:
  - `zsh`
  - Oh My Zsh
  - plugins (`$ZSH_CUSTOM`)
  - `powerlevel10k`
  - `Gogh` (terminal colors)

- Previously installed **Node.js + npm using `nvm` while on bash**

---

## ❗ Problem

Running:

```sh
npm run dev
```

Result:

```sh
zsh: command not found: npm
```

Even though:

```sh
echo $SHELL
```

Output:

```sh
/usr/bin/zsh
```

---

## ⚠️ Temporary Hack (Not Recommended)

```sh
source ~/.bashrc
```

This made `npm` work **temporarily**, but caused errors like:

```sh
command not found: shopt
```

### ❌ Why this is bad:

- `.bashrc` is for **bash**, not zsh
- Leads to incompatibilities and unstable shell behavior

---

## 🧠 Root Cause

- `nvm`, `node`, and `npm` were configured inside:

```sh
~/.bashrc
```

- But **zsh does NOT read `.bashrc`**
- zsh uses:

```sh
~/.zshrc
```

So:

- `nvm` ❌ not loaded
- `node` ❌ not found
- `npm` ❌ not found

---

## ✅ Proper Solution

### 1. Copy `nvm` config from `.bashrc`

```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

### 2. Paste into:

```sh
~/.zshrc
```

### 3. Reload zsh:

```sh
source ~/.zshrc
```

---

## 🔍 Verification

```sh
nvm --version
node -v
npm -v
```

All should now work ✅

---

## ⚙️ What Actually Happened (Deep Explanation)

The key line:

```sh
. "$NVM_DIR/nvm.sh"
```

This uses `source` (or `.`), which:

> Executes the script **inside the current shell (currently whcih is zsh)**

---

### 💡 Why `npm` suddenly works

Because now the shell knows where to find it:

```sh
~/.nvm/versions/node/vXX.X.X/bin/npm
```

Before:

- Path not included ❌

After:

- Path included ✅

---

## 🧠 Core Concept

> Tools don’t need to be reinstalled — they need to be **discoverable via `$PATH`**

---

## 🎭 Analogy (Police & Criminals)

```
police: you are under arrest.
criminal1 (nvm): wait… why only me?

my two partners are here too:
- node
- npm
```

### Interpretation:

- `nvm` = the main guy
- `node` + `npm` = hidden accomplices
- zsh initially couldn’t see any of them

When `nvm.sh` is sourced:

- `nvm` exposes their location
- adds them to `$PATH`
- suddenly all are “caught” (available)

---

## 🔁 Mental Model

1. zsh starts
2. `.zshrc` runs
3. `nvm.sh` is sourced
4. `nvm` modifies `$PATH`
5. `node` + `npm` become available

---

## 🚫 Common Mistake to Avoid

Do NOT do:

```sh
source ~/.bashrc
```

inside zsh long-term.

---

## 🧾 Final Takeaway

Switching shells does NOT carry over environment configs automatically.

You must explicitly migrate:

- environment variables
- tool initializations (like `nvm`)

---

## 🧠 One-Liner Summary

> “nvm was always installed — zsh just didn’t know where to look.”
