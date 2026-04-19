# Ryan CV DevOps Learning Guide — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a new standalone repo at `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/` containing a pre-built minimal HTML/CSS/JS CV template and a comprehensive README.md that teaches Ryan platform engineering from scratch through two deployment phases: GitHub Pages → AWS EC2 via Docker + Terraform.

**Architecture:** The deliverable is two things: (1) a minimal, pre-styled CV template Ryan customises but does not write, and (2) a linear narrative README that uses that CV project as the thread through every technology. Every chapter produces a visible real change. "What just happened?" callouts follow every key action.

**Tech Stack:** Static HTML/CSS/JS (no frameworks), nginx (Docker), GitHub Actions (CI/CD), GitHub Pages, Cloudflare DNS, AWS EC2 + Elastic IP + Security Group, Terraform, optional Kubernetes overview.

**Output repo:** `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/` — this is a SEPARATE new repo, not the Freiha-Repository where this plan lives. All file creation tasks target that path.

---

## File Map

| File | Task | Description |
|------|------|-------------|
| `ryan-cv-guide/index.html` | Task 1 | Pre-built CV template |
| `ryan-cv-guide/styles.css` | Task 2 | Clean professional styling with dark mode CSS variables |
| `ryan-cv-guide/script.js` | Task 3 | Dark mode toggle with localStorage persistence |
| `ryan-cv-guide/README.md` | Tasks 4–16 | Full learning guide, built chapter by chapter |

---

## Task 1: Create the repo directory and index.html

**Files:**
- Create: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/index.html`

- [ ] **Step 1: Create the directory**

```bash
mkdir -p /c/Users/Ghadi/IdeaProjects/ryan-cv-guide
cd /c/Users/Ghadi/IdeaProjects/ryan-cv-guide
```

- [ ] **Step 2: Create index.html**

Create `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/index.html` with this exact content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Ryan Freiha — CV</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <header>
    <div class="header-inner">
      <h1>Ryan Freiha</h1>
      <p class="title">Software Engineer</p>
      <p class="location">📍 London, UK</p>
      <nav class="contact-links">
        <a href="mailto:ryan@example.com">ryan@example.com</a>
        <a href="https://github.com/ryanfreiha" target="_blank">GitHub</a>
        <a href="https://linkedin.com/in/ryanfreiha" target="_blank">LinkedIn</a>
      </nav>
      <button id="theme-toggle" aria-label="Toggle dark mode">🌙</button>
    </div>
  </header>

  <main>
    <section id="about">
      <h2>About</h2>
      <p>
        Computer Science student with a passion for building things that work.
        Currently learning platform engineering, cloud infrastructure, and how
        the internet actually works under the hood.
      </p>
    </section>

    <section id="skills">
      <h2>Skills</h2>
      <ul class="skill-list">
        <li>Python</li>
        <li>JavaScript</li>
        <li>HTML &amp; CSS</li>
        <li>Git</li>
        <li>Docker</li>
        <li>Linux</li>
      </ul>
    </section>

    <section id="experience">
      <h2>Experience</h2>
      <div class="experience-item">
        <div class="exp-header">
          <strong>Junior Developer</strong>
          <span class="date">Jun 2024 – Sep 2024</span>
        </div>
        <p class="company">Some Company Ltd · Internship</p>
        <p>Worked on frontend features, learned version control in a team, fixed bugs.</p>
      </div>
    </section>

    <section id="education">
      <h2>Education</h2>
      <div class="experience-item">
        <div class="exp-header">
          <strong>BSc Computer Science</strong>
          <span class="date">2023 – 2026</span>
        </div>
        <p class="company">University Name</p>
      </div>
    </section>

    <section id="contact">
      <h2>Contact</h2>
      <p>Feel free to reach out: <a href="mailto:ryan@example.com">ryan@example.com</a></p>
    </section>
  </main>

  <footer>
    <p>Built and deployed by Ryan Freiha · <a href="https://github.com/ryanfreiha/ryan-cv">View source</a></p>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

- [ ] **Step 3: Verify**

Open `index.html` directly in a browser (double-click). You should see a plain, unstyled page with all sections visible. That's correct — styles come in Task 2.

---

## Task 2: Create styles.css

**Files:**
- Create: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/styles.css`

- [ ] **Step 1: Create styles.css**

```css
/* ── CSS custom properties — the foundation of our dark mode toggle ── */
:root {
  --bg: #ffffff;
  --surface: #f4f4f5;
  --text: #18181b;
  --muted: #71717a;
  --accent: #2563eb;
  --border: #e4e4e7;
  --radius: 8px;
  --max-width: 720px;
}

[data-theme="dark"] {
  --bg: #09090b;
  --surface: #18181b;
  --text: #fafafa;
  --muted: #a1a1aa;
  --accent: #60a5fa;
  --border: #27272a;
}

/* ── Reset & base ── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  background: var(--bg);
  color: var(--text);
  line-height: 1.6;
  transition: background 0.2s, color 0.2s;
}

a { color: var(--accent); text-decoration: none; }
a:hover { text-decoration: underline; }

/* ── Header ── */
header {
  background: var(--surface);
  border-bottom: 1px solid var(--border);
  padding: 2rem 1rem;
}

.header-inner {
  max-width: var(--max-width);
  margin: 0 auto;
  position: relative;
}

header h1 { font-size: 2rem; font-weight: 700; }
.title { font-size: 1.1rem; color: var(--accent); font-weight: 500; margin-top: 0.25rem; }
.location { color: var(--muted); font-size: 0.9rem; margin-top: 0.25rem; }

.contact-links {
  display: flex;
  gap: 1rem;
  margin-top: 0.75rem;
  flex-wrap: wrap;
}

#theme-toggle {
  position: absolute;
  top: 0;
  right: 0;
  background: none;
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 0.4rem 0.6rem;
  cursor: pointer;
  font-size: 1.1rem;
  color: var(--text);
  transition: background 0.2s;
}
#theme-toggle:hover { background: var(--border); }

/* ── Main content ── */
main {
  max-width: var(--max-width);
  margin: 0 auto;
  padding: 2rem 1rem;
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
}

section h2 {
  font-size: 1.2rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--muted);
  border-bottom: 1px solid var(--border);
  padding-bottom: 0.4rem;
  margin-bottom: 1rem;
}

/* ── Skills ── */
.skill-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  list-style: none;
}

.skill-list li {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 0.3rem 0.75rem;
  font-size: 0.9rem;
}

/* ── Experience & Education ── */
.experience-item { margin-bottom: 1.25rem; }

.exp-header {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.date { font-size: 0.85rem; color: var(--muted); }
.company { color: var(--muted); font-size: 0.9rem; margin: 0.15rem 0 0.4rem; }

/* ── Footer ── */
footer {
  text-align: center;
  padding: 2rem 1rem;
  color: var(--muted);
  font-size: 0.85rem;
  border-top: 1px solid var(--border);
}
```

- [ ] **Step 2: Verify**

Reload `index.html` in the browser. The CV should now look clean and professional — name large at top, sections separated, skills as pill tags. No dark mode yet (that's Task 3).

---

## Task 3: Create script.js

**Files:**
- Create: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/script.js`

- [ ] **Step 1: Create script.js**

```javascript
const toggle = document.getElementById('theme-toggle');
const root = document.documentElement;

// Restore saved preference on load
const saved = localStorage.getItem('theme');
if (saved) {
  root.setAttribute('data-theme', saved);
  toggle.textContent = saved === 'dark' ? '☀️' : '🌙';
}

toggle.addEventListener('click', () => {
  const isDark = root.getAttribute('data-theme') === 'dark';
  const next = isDark ? 'light' : 'dark';
  root.setAttribute('data-theme', next);
  toggle.textContent = next === 'dark' ? '☀️' : '🌙';
  localStorage.setItem('theme', next);
});
```

- [ ] **Step 2: Verify**

Reload `index.html`. Click the 🌙 button — the page should switch to dark mode instantly. Refresh — it should remember the preference. Click again — back to light.

- [ ] **Step 3: Commit the template as the starting commit**

```bash
cd /c/Users/Ghadi/IdeaProjects/ryan-cv-guide
git init
git add index.html styles.css script.js
git commit -m "initial: add CV template"
```

Expected output: `[main (root-commit) xxxxxxx] initial: add CV template` with 3 files changed.

---

## Task 4: README — Header, Introduction & Guide Structure

**Files:**
- Create: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md`

This task creates the README skeleton with the introduction and table of contents. Subsequent tasks append each chapter.

- [ ] **Step 1: Create README.md with header and intro**

Create `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md` with this exact content:

````markdown
# 🚀 Ryan's Platform Engineering Learning Guide

> A project-based journey from zero to shipping real infrastructure — using your personal CV website as the thread.

You're going to build, ship, and re-ship one project through every layer of the modern engineering stack. By the end, your CV will be live at **ryan.freiha.dev**, running in a Docker container on an AWS server you provisioned with Terraform.

This guide is split into two phases:

| Phase | What you build | What you learn |
|-------|---------------|----------------|
| **Phase 1** | CV live on GitHub Pages with custom domain | Git, GitHub, DNS, Bash, Networking, CI/CD |
| **Phase 2** | CV re-deployed to AWS via Docker + Terraform | Containers, Cloud, IaC, DNS migration |

**A note on the CV:** The template is already written for you — your job is to fill in your real details and learn to ship it. The content doesn't matter. The process does.

---

## Table of Contents

**Phase 1 — Ship It Fast**
- [Chapter 0: Prerequisites & Setup](#chapter-0-prerequisites--setup)
- [Chapter 1: Git & GitHub](#chapter-1-git--github)
- [Chapter 2: GitHub Pages](#chapter-2-github-pages)
- [Chapter 3: Custom Domain with Cloudflare](#chapter-3-custom-domain-with-cloudflare)
- [Chapter 4: Bash & Linux](#chapter-4-bash--linux)
- [Chapter 5: Networking Deep Dive](#chapter-5-networking-deep-dive)
- [Chapter 6: GitHub Actions & CI/CD](#chapter-6-github-actions--cicd)

**Phase 2 — Ship It Properly**
- [Chapter 7: Docker & Containers](#chapter-7-docker--containers)
- [Chapter 8: AWS Basics](#chapter-8-aws-basics)
- [Chapter 9: Terraform — Infrastructure as Code](#chapter-9-terraform--infrastructure-as-code)
- [Chapter 10: Deploy to EC2](#chapter-10-deploy-to-ec2)
- [Chapter 11: Point the Domain to AWS](#chapter-11-point-the-domain-to-aws)
- [Chapter 12: Kubernetes — Light Overview (Optional)](#chapter-12-kubernetes--light-overview-optional)

---
````

- [ ] **Step 2: Commit**

```bash
cd /c/Users/Ghadi/IdeaProjects/ryan-cv-guide
git add README.md
git commit -m "docs: add README skeleton and table of contents"
```

---

## Task 5: README — Chapter 0 (Prerequisites & Setup)

**Files:**
- Modify: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md` (append)

- [ ] **Step 1: Append Chapter 0 to README.md**

Append the following to `README.md`:

````markdown
---

# Phase 1 — Ship It Fast

---

## Chapter 0: Prerequisites & Setup

Before you write a single line, you need your tools. This chapter gets your Mac set up exactly the way professional engineers do it.

### 0.1 Install Homebrew

Homebrew is a **package manager** — a tool that installs other tools. Think of it as the App Store for the terminal.

Open **Terminal** (Cmd + Space → type "Terminal" → Enter) and run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**What this command does:**
- `curl -fsSL <url>` — downloads the install script from the internet silently (`-s`) and fails loudly if anything goes wrong (`-f`, `-L` follows redirects)
- `/bin/bash -c "..."` — passes the downloaded script directly to bash to run it

After installation, verify:

```bash
brew --version
```

Expected output: `Homebrew 4.x.x`

> ⚡ **What just happened?** Homebrew installed itself into `/opt/homebrew` (on Apple Silicon) or `/usr/local` (Intel). It also added itself to your PATH — the list of directories your shell searches when you type a command. Every tool you install with `brew install` becomes available system-wide.

### 0.2 Install Git

```bash
brew install git
git --version
```

Expected output: `git version 2.x.x`

Now configure your identity — Git attaches your name and email to every commit you make. This is public on GitHub:

```bash
git config --global user.name "Ryan Freiha"
git config --global user.email "your@email.com"
git config --global init.defaultBranch main
```

**What these do:**
- `--global` — saves to `~/.gitconfig` (your home directory), applies to every repo on your machine
- `init.defaultBranch main` — makes new repos start on `main` instead of the old default `master`

Verify your config:

```bash
git config --list
```

### 0.3 Install Visual Studio Code

VS Code is a lightweight, fast code editor — perfect for web files and scripts.

```bash
brew install --cask visual-studio-code
```

Open VS Code, then install these extensions (Cmd + Shift + X to open Extensions):
- **GitLens** — shows git blame, history, and diff inline in your editor
- **Prettier** — auto-formats your code on save
- **Live Server** — right-click `index.html` → "Open with Live Server" to auto-reload on save

Enable "Format on Save": Cmd + Shift + P → "Open User Settings (JSON)" → add:
```json
"editor.formatOnSave": true
```

### 0.4 Install IntelliJ IDEA (Student License)

IntelliJ is JetBrains' flagship IDE — heavy-duty, with deep language support. Great for Java, Kotlin, Python projects. VS Code is better for quick web/script work; IntelliJ is better for larger structured projects.

**Activate your free student license:**
1. Go to [jetbrains.com/student](https://www.jetbrains.com/community/education/#students)
2. Click **Apply Now** → select **GitHub** as your verification method
3. Sign in with your GitHub account — JetBrains checks your student status automatically via GitHub Education
4. Once approved, you'll receive an email with a license key
5. Download **IntelliJ IDEA Ultimate** from [jetbrains.com/idea](https://www.jetbrains.com/idea/)
6. On first launch: **Activate** → **JetBrains Account** → sign in

> 💡 **VS Code vs IntelliJ:** Use VS Code for this guide (HTML, CSS, Bash scripts, YAML). Use IntelliJ when you work on Java/Kotlin/Spring projects. Both are free for you as a student.

### 0.5 Connect to GitHub

You already have a GitHub account. Let's make sure your Mac can talk to it without typing your password every time, using an SSH key.

**Check if you already have an SSH key:**
```bash
ls ~/.ssh
```

If you see `id_ed25519` and `id_ed25519.pub`, skip to the "Add to GitHub" step.

**Generate a new key:**
```bash
ssh-keygen -t ed25519 -C "your@email.com"
```
Press Enter three times to accept defaults (no passphrase for simplicity).

**Add the public key to GitHub:**
```bash
cat ~/.ssh/id_ed25519.pub
```
Copy the output. Go to **GitHub → Settings → SSH and GPG keys → New SSH key**. Paste it in.

**Test the connection:**
```bash
ssh -T git@github.com
```
Expected: `Hi ryanfreiha! You've successfully authenticated`

> ⚡ **What just happened?** You created a key pair — a private key (stays on your Mac, never shared) and a public key (given to GitHub). When you push code, your Mac proves its identity by solving a cryptographic challenge that only the holder of the private key can solve. No password needed.

````

- [ ] **Step 2: Commit**

```bash
cd /c/Users/Ghadi/IdeaProjects/ryan-cv-guide
git add README.md
git commit -m "docs: add chapter 0 - prerequisites and setup"
```

---

## Task 6: README — Chapter 1 (Git & GitHub)

**Files:**
- Modify: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md` (append)

- [ ] **Step 1: Append Chapter 1**

````markdown
---

## Chapter 1: Git & GitHub — Your Code's Time Machine

Git is a **version control system** — it tracks every change to every file, who made it, and when. GitHub is a website that hosts Git repositories so you can back them up and share them.

> 💡 **Why this matters:** Without Git, you'd be saving files like `cv_final_FINAL_v3_actualfinal.html`. With Git, you have a complete history of every change, the ability to undo anything, and a way to collaborate with others without overwriting each other's work.

### 1.1 Create a GitHub Repository

1. Go to [github.com](https://github.com) → click **+** → **New repository**
2. Name it `ryan-cv`
3. Set it to **Public** (required for free GitHub Pages)
4. **Do NOT** check "Add a README" — we already have our files locally
5. Click **Create repository**

GitHub will show you a page with setup instructions. Copy the SSH remote URL — it looks like `git@github.com:ryanfreiha/ryan-cv.git`.

### 1.2 Connect Your Local Files to GitHub

Navigate to your CV folder in the terminal:

```bash
cd /path/to/ryan-cv-guide
```

If you followed Task 3, you already ran `git init`. Let's verify:

```bash
git status
```

Expected output:
```
On branch main
nothing to commit, working tree clean
```

Add the GitHub repo as your remote:

```bash
git remote add origin git@github.com:ryanfreiha/ryan-cv.git
```

**What this command does:**
- `git remote add` — registers a remote server for this repo
- `origin` — the conventional name for your primary remote (it's just a nickname)
- `git@github.com:...` — the SSH address of the repo on GitHub

Push your code:

```bash
git push -u origin main
```

**What the flags do:**
- `-u` — sets `origin main` as the default upstream for this branch. Future pushes only need `git push`
- `origin` — which remote to push to
- `main` — which branch to push

> ⚡ **What just happened?** Your three files now live in two places: your Mac and GitHub's servers. Every commit is permanently recorded with a unique hash (like `a3f9c21`), your name, your email, and a timestamp. You can never truly lose work again.

### 1.3 The Git Workflow — Understanding the Three Zones

This is the most important mental model in Git:

```
Working Directory  →  Staging Area  →  Repository
   (your files)       (git add)        (git commit)
```

- **Working Directory:** Files you're editing right now
- **Staging Area:** Changes you've selected to include in the next commit
- **Repository:** The permanent history of commits

**Why does the staging area exist?** So you can commit only *some* of your changes. You might edit 5 files but only want to commit 3 of them as one logical unit.

**Try it — make a change and watch the workflow:**

```bash
# Edit index.html — change "Ryan Freiha" to your actual name
# Then:

git status          # Shows the file as "modified" (working directory)
git diff            # Shows exactly what changed, line by line
git add index.html  # Moves change to staging area
git status          # Now shows "Changes to be committed"
git commit -m "personalise: update name in CV"
git push
```

**Reading `git log`:**

```bash
git log --oneline
```

Expected output:
```
b4d2a1f personalise: update name in CV
a3f9c21 initial: add CV template
```

Each line is a commit: hash (first 7 chars of the full SHA), then your message.

> 💡 **Write good commit messages:** Use the imperative mood ("add feature", not "added feature"). The message should complete the sentence "This commit will..." Keep it under 72 characters.

### 1.4 Branching (Quick Preview)

You won't need branches heavily in this guide, but you'll hear the word constantly:

```bash
git branch          # Lists branches (* = current)
git checkout -b my-feature  # Creates and switches to a new branch
git checkout main   # Switch back to main
```

A branch is just a pointer to a commit. Changes on a branch don't affect `main` until you merge them. This is how teams work without stepping on each other.

````

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add chapter 1 - git and github"
```

---

## Task 7: README — Chapter 2 (GitHub Pages)

**Files:**
- Modify: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md` (append)

- [ ] **Step 1: Append Chapter 2**

````markdown
---

## Chapter 2: GitHub Pages — Instant Hosting

GitHub Pages takes the files in your repository and serves them as a live website — for free. No servers to manage, no hosting bill.

> 💡 **What is "hosting"?** When someone visits a URL, their browser sends a request to a server asking for files. Hosting means having a server ready to respond with your files. GitHub Pages is GitHub's built-in server for static files (HTML, CSS, JS — no databases or backends).

### 2.1 Enable GitHub Pages

1. On your GitHub repo page → **Settings** tab
2. Sidebar → **Pages**
3. Under **Source**: select **Deploy from a branch**
4. Branch: `main`, Folder: `/ (root)`
5. Click **Save**

Wait 30–60 seconds, then visit:
```
https://ryanfreiha.github.io/ryan-cv
```

Your CV is live. 🎉

> ⚡ **What just happened?** GitHub detected your `index.html` and started serving it via their CDN (Content Delivery Network — a network of servers around the world). When someone visits the URL, GitHub's servers read your file and send it over HTTP to their browser. No backend, no database — just files traveling over the internet.

### 2.2 Explore What's Happening — Browser DevTools

Open your site in Chrome or Firefox. Press **F12** (or Cmd + Option + I on Mac) to open DevTools.

Click the **Network** tab, then refresh the page.

You'll see a list of requests. Click on `ryan-cv` (the first one):

- **Status:** `200` — success. (404 = not found, 500 = server error, 301 = redirect)
- **Request Method:** `GET` — you're asking for a file, not sending data
- **Response Headers:** Look for `content-type: text/html` — the server told your browser what kind of file it sent
- **Response:** Click the Response tab — there's your actual HTML

> 💡 **HTTP status codes you'll see everywhere:**
> - `200 OK` — everything worked
> - `301/302` — redirect (page moved)
> - `404 Not Found` — file doesn't exist
> - `500 Internal Server Error` — something broke on the server side

### 2.3 Push a Change and Watch it Deploy

```bash
# Edit something visible in index.html — add a line to the About section
git add index.html
git commit -m "content: add note to about section"
git push
```

Wait ~60 seconds, then refresh your GitHub Pages URL. See the change live.

Go to the **Actions** tab on your GitHub repo — you'll see GitHub's deployment pipeline running automatically. GitHub is re-reading your files and pushing them to their CDN after every push.

> ⚡ **What just happened?** You pushed code → GitHub detected the push → ran its deployment process → updated the CDN → your change is visible worldwide. This is the simplest form of a deployment pipeline. Chapter 6 teaches you to build and control this yourself.

````

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add chapter 2 - github pages"
```

---

## Task 8: README — Chapter 3 (Custom Domain)

**Files:**
- Modify: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md` (append)

- [ ] **Step 1: Append Chapter 3**

````markdown
---

## Chapter 3: Custom Domain with Cloudflare — ryan.freiha.dev

Right now your CV lives at `ryanfreiha.github.io/ryan-cv`. Let's move it to `ryan.freiha.dev`.

> 💡 **What is DNS?** The Domain Name System is the internet's phone book. When you type `ryan.freiha.dev`, your computer doesn't know where that is — it asks a chain of DNS servers to look it up and return an IP address. DNS records are the entries in that phone book.

### 3.1 Understand the DNS Record Types You'll Use

| Record Type | What it does |
|-------------|-------------|
| **A record** | Maps a name to an IPv4 address (e.g., `ryan.freiha.dev → 185.199.108.153`) |
| **CNAME record** | Maps a name to another name (alias) (e.g., `ryan.freiha.dev → ryanfreiha.github.io`) |
| **TTL** | Time To Live — how long (seconds) other DNS servers should cache this record before re-checking |

### 3.2 Add a CNAME File to Your Repo

GitHub Pages needs to know which custom domain is yours:

```bash
echo "ryan.freiha.dev" > CNAME
git add CNAME
git commit -m "config: add custom domain CNAME file"
git push
```

This file tells GitHub: "this repo owns `ryan.freiha.dev`."

### 3.3 Configure GitHub Pages Custom Domain

1. **Settings → Pages → Custom domain**
2. Type `ryan.freiha.dev`
3. Click **Save**

GitHub will show a warning that DNS isn't configured yet — that's fine, we're doing it next.

### 3.4 Add DNS Record in Cloudflare

The `freiha.dev` domain is already in Cloudflare. You need to add a subdomain for Ryan.

1. Log in to [cloudflare.com](https://cloudflare.com)
2. Select the `freiha.dev` zone
3. Go to **DNS → Records → Add record**
4. Set:
   - **Type:** `CNAME`
   - **Name:** `ryan`
   - **Target:** `ryanfreiha.github.io`
   - **Proxy status:** ☁️ **DNS only** (grey cloud, NOT orange)
   - **TTL:** Auto

> ⚡ **Why DNS only, not proxied?** GitHub Pages needs to verify that `ryan.freiha.dev` points to their servers so they can provision an HTTPS certificate (via Let's Encrypt). If Cloudflare's proxy is on, GitHub sees Cloudflare's IP, not your domain, and the certificate check fails. We'll enable the proxy in Phase 2 when we control the server.

### 3.5 Wait for DNS Propagation

DNS changes don't apply instantly — TTL means old records are cached globally. Watch it propagate:

```bash
# Run this a few times, 30 seconds apart
dig ryan.freiha.dev

# Look for the ANSWER SECTION:
# ryan.freiha.dev. 300 IN CNAME ryanfreiha.github.io.
```

**Reading the `dig` output:**
- `ryan.freiha.dev.` — the name you looked up
- `300` — TTL in seconds (this record is cached for 5 minutes)
- `IN` — Internet class (always IN for normal DNS)
- `CNAME` — record type
- `ryanfreiha.github.io.` — where it points

Once DNS propagates, GitHub auto-provisions HTTPS. Visit `https://ryan.freiha.dev` — your CV with a padlock.

### 3.6 Inspect the Full Chain

```bash
# See the full DNS resolution chain
dig ryan.freiha.dev +trace

# See the HTTP headers from the terminal
curl -I https://ryan.freiha.dev
```

**Reading the curl output:**
```
HTTP/2 200
content-type: text/html; charset=utf-8
server: GitHub.com
```

> ⚡ **What just happened?** When someone types `ryan.freiha.dev`:
> 1. Their computer asks their ISP's DNS resolver
> 2. That resolver asks Cloudflare's nameservers (authoritative for freiha.dev)
> 3. Cloudflare returns: "ryan.freiha.dev is a CNAME for ryanfreiha.github.io"
> 4. The resolver looks up ryanfreiha.github.io → gets GitHub's IP
> 5. Browser connects to GitHub's IP
> 6. GitHub sees the `Host: ryan.freiha.dev` header, finds your CNAME file, serves your CV

````

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add chapter 3 - custom domain and cloudflare dns"
```

---

## Task 9: README — Chapter 4 (Bash & Linux)

**Files:**
- Modify: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md` (append)

- [ ] **Step 1: Append Chapter 4**

````markdown
---

## Chapter 4: Bash & Linux — Living in the Terminal

The terminal is the primary interface for every technology in Phase 2. Engineers who are fluent in Bash can do in seconds what takes minutes in a GUI.

> 💡 **Bash is a shell** — a program that reads commands you type and runs them. macOS uses Zsh by default (a Bash-compatible shell). Linux servers typically use Bash. The commands below work on both.

### 4.1 Filesystem Navigation

```bash
pwd                 # Print Working Directory — where am I right now?
ls                  # List files in current directory
ls -la              # -l = long format (permissions, size, date), -a = include hidden files (starting with .)
cd ryan-cv          # Change Directory into ryan-cv folder
cd ..               # Go up one directory
cd ~                # Go to your home directory (/Users/yourname)
```

**Run these now in your CV project folder:**

```bash
cd /path/to/ryan-cv
ls -la
```

You'll see `.git/` — that hidden directory is Git's entire database for this repo. Never manually edit files inside it.

### 4.2 Reading Files

```bash
cat index.html          # Print entire file to terminal
head -n 20 index.html   # First 20 lines only
grep "Ryan" index.html  # Find lines containing "Ryan"
grep -n "section" index.html  # -n shows line numbers
```

**`grep` is one of the most-used tools in engineering.** On a server, you'll use it to search logs:
```bash
grep "ERROR" /var/log/nginx/error.log
grep -i "404" access.log   # -i = case insensitive
```

### 4.3 The Pipe — Unix's Superpower

The pipe `|` takes the output of one command and feeds it as input to the next:

```bash
cat index.html | grep "section"
# Same as: grep "section" index.html
# But now you can chain more:
cat index.html | grep "section" | wc -l   # Count matching lines
```

> ⚡ **What just happened?** You built a mini-pipeline: cat reads the file → grep filters lines → wc counts them. Three separate programs, chained with `|`, no glue code. This is the Unix philosophy: small tools that do one thing well, composed together.

### 4.4 curl — Make HTTP Requests from the Terminal

```bash
curl https://ryan.freiha.dev           # Fetch the HTML (prints to terminal)
curl -I https://ryan.freiha.dev        # -I = headers only (no body)
curl -v https://ryan.freiha.dev        # -v = verbose, shows full request + response + TLS details
curl -L https://ryan.freiha.dev        # -L = follow redirects
```

### 4.5 Environment Variables

Variables that programs read to configure themselves — instead of hardcoding values:

```bash
echo $HOME          # Print your home directory path
echo $PATH          # The directories your shell searches for commands
export MY_NAME="Ryan"     # Set a variable (available to child processes)
echo $MY_NAME
```

> 💡 **Why this matters for later:** In Chapter 6, GitHub Actions uses environment variables for secrets (API keys, passwords). In Chapter 8, the AWS CLI reads `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` from environment variables. You never hardcode secrets in files.

### 4.6 File Permissions

```bash
ls -la index.html
# -rw-r--r--  1 ryan staff  2048 Apr 19 12:00 index.html
```

Read the permissions string `-rw-r--r--`:
- First `-` — type (`-` = file, `d` = directory)
- `rw-` — owner can read and write, not execute
- `r--` — group can read only
- `r--` — everyone else can read only

```bash
chmod 644 index.html    # rw-r--r--  (standard for web files)
chmod 755 script.sh     # rwxr-xr-x  (executable by owner, readable by all)
chmod +x deploy.sh      # Add execute permission
```

### 4.7 Useful Shortcuts

```bash
Ctrl + C        # Kill the running process
Ctrl + L        # Clear terminal (same as `clear`)
Ctrl + R        # Search command history
!!              # Repeat last command
Tab             # Autocomplete file/command names
Up arrow        # Previous command
```

````

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add chapter 4 - bash and linux"
```

---

## Task 10: README — Chapter 5 (Networking Deep Dive)

**Files:**
- Modify: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md` (append)

- [ ] **Step 1: Append Chapter 5**

````markdown
---

## Chapter 5: Networking Deep Dive — What Actually Happens

You've set up a domain, pushed code, and watched your CV go live. This chapter explains the full journey — from typing `https://ryan.freiha.dev` to pixels appearing on screen.

### 5.1 The Full Stack of a Web Request

```
Your browser
    │
    ├─ 1. DNS Resolution         (find the IP address for ryan.freiha.dev)
    ├─ 2. TCP Connection         (establish a reliable connection to that IP)
    ├─ 3. TLS Handshake          (negotiate encryption — the S in HTTPS)
    ├─ 4. HTTP Request           (ask the server for the page)
    ├─ 5. HTTP Response          (server sends back the HTML)
    └─ 6. Render                 (browser parses HTML, loads CSS+JS, draws pixels)
```

### 5.2 Step 1: DNS Resolution

```bash
dig ryan.freiha.dev +trace
```

This shows the full resolution chain:

```
. (root)               → 13 root nameservers handle all of DNS
dev. (TLD)             → .dev nameservers know who controls *.dev domains
freiha.dev.            → Cloudflare's nameservers are authoritative here
ryan.freiha.dev.       → returns CNAME → ryanfreiha.github.io → GitHub's IP
```

**Every domain lookup follows this chain.** Results are cached at each step for the TTL duration — that's why DNS changes don't apply instantly.

### 5.3 Step 2: TCP/IP — The Reliable Pipe

IP (Internet Protocol) gets packets from A to B. TCP (Transmission Control Protocol) makes sure they all arrive, in order, without errors.

TCP starts with a **3-way handshake:**

```
Your Mac        →  SYN  →        GitHub's server
Your Mac        ←  SYN-ACK  ←   GitHub's server
Your Mac        →  ACK  →        GitHub's server
        [connection established — data flows]
```

- **SYN** — "I want to connect"
- **SYN-ACK** — "OK, I'm ready"
- **ACK** — "Great, let's go"

> 💡 **Why does TCP exist?** The internet is built on "best effort" packet delivery — packets can be lost, duplicated, or arrive out of order. TCP adds sequencing and acknowledgements on top so that higher-level protocols (like HTTP) can assume a reliable stream.

### 5.4 Step 3: TLS — Encrypted Channels

HTTPS = HTTP + TLS. The TLS handshake:
1. Server sends its **certificate** (proves it owns `ryan.freiha.dev`, signed by Let's Encrypt)
2. Your browser verifies the certificate against trusted Certificate Authorities
3. Both sides agree on a **session key** (symmetric encryption) for the rest of the connection
4. All data is encrypted — no one in the middle can read it

```bash
curl -v https://ryan.freiha.dev 2>&1 | grep -A 10 "SSL connection"
```

### 5.5 Step 4 & 5: HTTP Request/Response

```bash
curl -v https://ryan.freiha.dev 2>&1 | head -50
```

You'll see your browser's request:
```
> GET / HTTP/2
> Host: ryan.freiha.dev
> User-Agent: curl/8.x
> Accept: */*
```

And the server's response:
```
< HTTP/2 200
< content-type: text/html; charset=utf-8
< server: GitHub.com
```

**Key headers to understand:**
- `Host` — tells the server which site you want (multiple sites can share one IP)
- `User-Agent` — identifies the client (browser, curl, etc.)
- `Content-Type` — what format the response body is in
- `Cache-Control` — tells browsers/CDNs how long to cache the response

### 5.6 Trace the Route

```bash
traceroute ryan.freiha.dev
```

This shows every network hop between your Mac and GitHub's server — routers across the internet, each adding a tiny bit of latency.

> ⚡ **Tying it all together:** When you pushed your CV and watched it appear at `ryan.freiha.dev`, here's what happened at every layer:
> 1. DNS told browsers where GitHub's servers are
> 2. TCP opened a reliable connection to that server
> 3. TLS encrypted the channel
> 4. HTTP carried the request ("give me index.html") and the response (here it is)
> 5. Your browser parsed the HTML, fetched styles.css and script.js via separate HTTP requests, and rendered the page

````

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add chapter 5 - networking deep dive"
```

---

## Task 11: README — Chapter 6 (GitHub Actions & CI/CD)

**Files:**
- Modify: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md` (append)

- [ ] **Step 1: Append Chapter 6**

````markdown
---

## Chapter 6: GitHub Actions & CI/CD — Automated Everything

Right now you deploy by: edit → `git push`. GitHub Pages picks it up automatically. But in real engineering, you want automated checks (catch broken code before it goes live) and a controlled deployment process. That's CI/CD.

> 💡 **CI/CD defined:**
> - **Continuous Integration (CI):** Every push automatically runs tests and checks. Broken code is caught before it reaches production.
> - **Continuous Deployment (CD):** If CI passes, the code is automatically deployed. No manual steps.

### 6.1 GitHub Actions Concepts

| Concept | What it is |
|---------|-----------|
| **Workflow** | A YAML file in `.github/workflows/` that defines automation |
| **Trigger** | What starts the workflow (a push, a PR, a schedule, manual) |
| **Job** | A group of steps that run on one machine |
| **Step** | A single command or action within a job |
| **Runner** | A fresh virtual machine GitHub spins up to run your job |
| **Action** | A reusable step packaged by the community (e.g., `actions/checkout`) |

### 6.2 Create Your First Workflow

```bash
mkdir -p .github/workflows
```

Create `.github/workflows/deploy.yml`:

```yaml
name: Validate and Deploy CV

on:
  push:
    branches: [main]    # Trigger: only when pushing to main

jobs:
  validate:
    name: Validate HTML
    runs-on: ubuntu-latest   # Runner: a fresh Ubuntu VM

    steps:
      - name: Checkout code
        uses: actions/checkout@v4   # Clones your repo onto the runner

      - name: Validate HTML structure
        run: |
          # Check that index.html exists and contains required sections
          test -f index.html || (echo "index.html missing!" && exit 1)
          grep -q "<title>" index.html || (echo "Missing <title> tag" && exit 1)
          grep -q "id=\"about\"" index.html || (echo "Missing about section" && exit 1)
          echo "✅ HTML validation passed"

  deploy:
    name: Deploy to GitHub Pages
    runs-on: ubuntu-latest
    needs: validate    # Only runs if validate job succeeds
    permissions:
      pages: write
      id-token: write

    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Pages
        uses: actions/configure-pages@v4

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'      # Upload the entire repo root

      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

**What every line does:**

- `on: push: branches: [main]` — this workflow fires whenever code is pushed to `main`
- `runs-on: ubuntu-latest` — GitHub spins up a fresh Ubuntu VM for each run. It's destroyed after.
- `uses: actions/checkout@v4` — a community action that clones your repo into the VM
- `run: |` — runs multi-line shell commands
- `needs: validate` — `deploy` won't run unless `validate` succeeds
- `permissions:` — GitHub requires explicit permissions to deploy to Pages

### 6.3 Enable Pages from Actions

Go to **Settings → Pages → Source** and change it from "Deploy from branch" to **"GitHub Actions"**. Now Pages is controlled by your workflow, not automatically.

### 6.4 Push and Watch

```bash
git add .github/
git commit -m "ci: add validation and deployment workflow"
git push
```

Go to the **Actions** tab on GitHub. You'll see your workflow running. Click into it — watch each step execute in real time with full logs.

> ⚡ **What just happened?** You just automated your entire deployment. Every push to `main`:
> 1. GitHub spins up a fresh Ubuntu VM
> 2. Checks out your code
> 3. Validates your HTML
> 4. If valid, deploys to Pages
> 5. Tears down the VM
> You never manually deploy again.

### 6.5 Break It on Purpose

```bash
# Remove the about section id from index.html temporarily
# Change: <section id="about"> to <section id="oops">
git add index.html
git commit -m "test: intentionally break validation"
git push
```

Watch the Action fail. Read the error in the logs. Fix it, push again — watch it go green.

> 💡 **This is the power of CI:** The broken code never reached your live site. The validate job caught it first and blocked the deploy job.

### 6.6 Secrets — Never Put Keys in Code

In Phase 2, GitHub Actions needs AWS credentials. Never put them in YAML files — they'd be public.

Go to **Settings → Secrets and variables → Actions → New repository secret**.

In a workflow, you reference them as:
```yaml
env:
  AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
```

Secrets are encrypted, never shown in logs (masked as `***`), and only available to workflow runs on your repo.

````

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add chapter 6 - github actions and ci/cd"
```

---

## Task 12: README — Chapter 7 (Docker & Containers)

**Files:**
- Modify: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md` (append)

- [ ] **Step 1: Append Chapter 7**

````markdown
---

# Phase 2 — Ship It Properly

> GitHub Pages is great for static sites. But most real applications need a server you control — for APIs, databases, custom logic, or scale. In Phase 2, you'll deploy the exact same CV on real cloud infrastructure, the same way companies run their services.

---

## Chapter 7: Docker & Containers — Packaging Your App

> 💡 **The problem Docker solves:** "It works on my machine" — a phrase that has caused countless production incidents. Docker packages your application and everything it needs to run (OS libraries, configs, dependencies) into a single portable unit called a **container**.

### 7.1 VMs vs Containers

```
Virtual Machine:                    Container:
┌─────────────┐                    ┌───────────┐ ┌───────────┐
│  Your App   │                    │  Your App │ │ Other App │
├─────────────┤                    ├───────────┤ ├───────────┤
│  Guest OS   │                    │ Container │ │ Container │
│  (full OS!) │                    │  Runtime  │ │  Runtime  │
├─────────────┤                    ├───────────┴─┴───────────┤
│ Hypervisor  │                    │      Host OS Kernel      │
├─────────────┤                    ├──────────────────────────┤
│  Hardware   │                    │        Hardware          │
└─────────────┘                    └──────────────────────────┘
~Minutes to start, GBs             ~Milliseconds to start, MBs
```

Containers share the host OS kernel — they don't each run a full OS. That makes them tiny and fast.

### 7.2 Install Docker Desktop

```bash
brew install --cask docker
```

Open Docker Desktop from Applications. Wait for the whale icon in the menu bar to stop animating (Docker is ready).

Verify:
```bash
docker --version
docker run hello-world
```

Expected: a message saying "Hello from Docker!"

> ⚡ **What just happened?** Docker pulled an image called `hello-world` from Docker Hub (a public registry), created a container from it, ran it, printed the message, and stopped. The whole thing was ~100ms.

### 7.3 Key Docker Concepts

| Concept | What it is |
|---------|-----------|
| **Image** | A read-only template (like a class in OOP) |
| **Container** | A running instance of an image (like an object) |
| **Dockerfile** | Instructions for building an image |
| **Layer** | Each instruction in a Dockerfile adds a layer — layers are cached |
| **Registry** | A server that stores images (Docker Hub, GitHub Container Registry, AWS ECR) |

### 7.4 Write a Dockerfile

Create `Dockerfile` in your CV project root:

```dockerfile
FROM nginx:alpine

COPY . /usr/share/nginx/html

EXPOSE 80
```

**What each line does:**
- `FROM nginx:alpine` — start from the official nginx image built on Alpine Linux (tiny, ~5MB). This is your base layer.
- `COPY . /usr/share/nginx/html` — copy all your files into the directory nginx serves by default
- `EXPOSE 80` — documents that this container listens on port 80 (HTTP). This is metadata — it doesn't open ports on its own.

### 7.5 Build and Run

```bash
# Build the image, tag it as "ryan-cv"
docker build -t ryan-cv .

# List your images
docker images

# Run a container from it, mapping port 8080 on your Mac to port 80 in the container
docker run -p 8080:80 ryan-cv
```

Visit `http://localhost:8080` — your CV served by nginx inside a container.

**Port mapping explained:** `-p 8080:80` means "forward traffic from `localhost:8080` on my Mac to port `80` inside the container." nginx listens on 80 inside, but you access it from 8080 outside.

Press `Ctrl + C` to stop.

### 7.6 Run in the Background + Container Commands

```bash
docker run -d -p 8080:80 ryan-cv     # -d = detached (background)
docker ps                             # List running containers
docker logs <container-id>           # See nginx access logs
docker exec -it <container-id> sh    # Open a shell INSIDE the running container
docker stop <container-id>           # Stop it
docker rm <container-id>             # Remove the stopped container
```

**Try `docker exec -it <id> sh`** — you're now inside the container. Run `ls /usr/share/nginx/html` — there are your files. Run `exit` to leave.

> ⚡ **What just happened?** You packaged your CV and an entire web server into a single portable artifact. Run this on any Linux server with Docker installed and it behaves identically. No "install nginx, configure it, copy files" — just `docker run`.

### 7.7 Volume Mount for Local Development

When building, your files are baked into the image. To edit files and see changes without rebuilding:

```bash
docker run -d -p 8080:80 -v $(pwd):/usr/share/nginx/html nginx:alpine
```

`-v $(pwd):/usr/share/nginx/html` — mounts your current directory into the container at runtime. Edit `index.html`, refresh the browser — changes appear immediately.

> 💡 **Image vs Volume:** With `docker build`, files are baked in (immutable image). With `-v`, files are mounted from your host at runtime (live updates). Use `-v` for development, build images for production.

```bash
git add Dockerfile
git commit -m "docker: add Dockerfile for nginx"
```

````

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add chapter 7 - docker and containers"
```

---

## Task 13: README — Chapter 8 (AWS Basics)

**Files:**
- Modify: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md` (append)

- [ ] **Step 1: Append Chapter 8**

````markdown
---

## Chapter 8: AWS — Real Cloud Infrastructure

> 💡 **What is the cloud?** Someone else's computers — but available on-demand, billed by the second, and globally distributed. AWS (Amazon Web Services) is the largest cloud provider. You'll use it to rent a virtual server and run your Docker container on it.

### 8.1 Create an AWS Account

1. Go to [aws.amazon.com](https://aws.amazon.com) → **Create an AWS Account**
2. Follow the signup flow (requires a credit card — free tier means $0 for t2.micro)
3. **Immediately enable MFA on your root account:**
   - Top-right menu → **Security credentials**
   - **Multi-factor Authentication → Assign MFA device**
   - Use an authenticator app (Google Authenticator, Authy)

> ⚡ **Why MFA on root immediately?** The root account has unlimited access to everything — it can delete all your data, run up a $10,000 bill, delete itself. If someone steals your password without MFA, they own your account. Root should almost never be used for daily work — that's what IAM is for.

### 8.2 IAM — Identity and Access Management

IAM controls who can do what in your AWS account.

**Create an IAM user for daily use:**
1. Search "IAM" in the AWS console
2. **Users → Create user**
3. Name: `ryan-admin`
4. Check: **Provide user access to the AWS Management Console**
5. Permissions: **Attach policies directly** → `AdministratorAccess`
6. Download the CSV with credentials

> 💡 **Principle of Least Privilege:** In production, IAM users and roles should only have exactly the permissions they need — not AdministratorAccess. For learning, Admin is fine. But the concept matters: if an IAM key is leaked, blast radius is limited to what that user can do.

**Create an access key (for CLI use):**
1. Click your new user → **Security credentials → Create access key**
2. Select **Command Line Interface (CLI)**
3. Download the CSV — store it safely, you can't see the secret again

### 8.3 AWS CLI

```bash
brew install awscli
aws configure
```

Enter when prompted:
```
AWS Access Key ID: <from CSV>
AWS Secret Access Key: <from CSV>
Default region name: eu-west-1        # Or us-east-1 — pick closest to you
Default output format: json
```

Test:
```bash
aws sts get-caller-identity
```

Expected output:
```json
{
    "UserId": "AIDA...",
    "Account": "123456789012",
    "Arn": "arn:aws:iam::123456789012:user/ryan-admin"
}
```

> ⚡ **What just happened?** The CLI read your credentials from `~/.aws/credentials` and made an API call to AWS to verify who you are. Every AWS CLI command is an HTTPS API request under the hood — the CLI is just a convenient wrapper.

### 8.4 Key AWS Concepts

| Concept | What it is |
|---------|-----------|
| **Region** | A geographic location (eu-west-1 = Ireland). Resources live in regions. |
| **Availability Zone (AZ)** | A data centre within a region. Multiple AZs = redundancy. |
| **EC2** | Elastic Compute Cloud — virtual servers you rent by the hour |
| **t2.micro** | EC2 instance type: 1 vCPU, 1GB RAM. Free tier eligible for 12 months. |
| **AMI** | Amazon Machine Image — the OS template for your EC2 instance (like a Docker image for a VM) |
| **Security Group** | A virtual firewall — controls which ports accept inbound/outbound traffic |
| **Key Pair** | SSH keys managed by AWS — needed to connect to EC2 instances |
| **Elastic IP** | A static public IP that stays the same even if the instance restarts |

````

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add chapter 8 - aws basics"
```

---

## Task 14: README — Chapter 9 (Terraform)

**Files:**
- Modify: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md` (append)

- [ ] **Step 1: Append Chapter 9**

````markdown
---

## Chapter 9: Terraform — Infrastructure as Code

> 💡 **What is IaC?** Instead of clicking through the AWS console to create servers, you write code that describes what infrastructure you want. Terraform reads that code and creates it. This means your infrastructure is version-controlled, reproducible, and auditable — just like your application code.

### 9.1 Install Terraform

```bash
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
terraform --version
```

### 9.2 Declarative vs Imperative

| Imperative (step-by-step) | Declarative (describe the end state) |
|--------------------------|--------------------------------------|
| "Create an EC2 instance, then create a security group, then attach it" | "I want an EC2 instance with this security group" |
| Order matters | Terraform figures out the order |
| Hard to reproduce | Run it again → same result |

### 9.3 Create the Terraform Config

Create a `terraform/` directory in your CV project:

```bash
mkdir terraform
```

Create `terraform/main.tf`:

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "eu-west-1"   # Change to your preferred region
}

# SSH Key Pair — uses your existing public key
resource "aws_key_pair" "ryan_key" {
  key_name   = "ryan-cv-key"
  public_key = file("~/.ssh/id_ed25519.pub")
}

# Security Group — the firewall rules
resource "aws_security_group" "ryan_cv_sg" {
  name        = "ryan-cv-sg"
  description = "Allow SSH and HTTP"

  ingress {
    description = "SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]   # In production, lock this to your IP
  }

  ingress {
    description = "HTTP"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"             # Allow all outbound
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# EC2 Instance — Amazon Linux 2023, t2.micro (free tier)
resource "aws_instance" "ryan_cv" {
  ami                    = "ami-0905a3c97561e0b69"   # Amazon Linux 2023 in eu-west-1
  instance_type          = "t2.micro"
  key_name               = aws_key_pair.ryan_key.key_name
  vpc_security_group_ids = [aws_security_group.ryan_cv_sg.id]

  tags = {
    Name = "ryan-cv-server"
  }
}

# Elastic IP — a static public IP that survives instance restarts
resource "aws_eip" "ryan_cv_eip" {
  instance = aws_instance.ryan_cv.id
  domain   = "vpc"
}

# Output the IP so we can use it
output "server_ip" {
  value       = aws_eip.ryan_cv_eip.public_ip
  description = "Public IP of the CV server — use this for DNS"
}
```

**What each block does:**

- `terraform {}` — declares which providers (plugins) this config needs
- `provider "aws"` — configures the AWS provider with your region. It reads credentials from `~/.aws/credentials` automatically.
- `aws_key_pair` — uploads your SSH public key to AWS so EC2 can accept your connections
- `aws_security_group` — creates firewall rules. Port 22 = SSH, Port 80 = HTTP
- `aws_instance` — the actual virtual server. `ami` is the OS image ID.
- `aws_eip` — a static IP. Without this, the public IP changes every time the instance restarts, breaking DNS.
- `output` — after apply, Terraform prints this value to the terminal

### 9.4 Run Terraform

```bash
cd terraform

terraform init
```

Expected: downloads the AWS provider plugin into `.terraform/`

```bash
terraform plan
```

Expected: a diff showing everything Terraform will create. Read it carefully — this is your preview before anything real happens. It shows `+` for resources to create.

```bash
terraform apply
```

Type `yes` when prompted. Terraform creates:
1. The key pair
2. The security group
3. The EC2 instance
4. The Elastic IP

Expected output at the end:
```
Apply complete! Resources: 4 added, 0 changed, 0 destroyed.

Outputs:
server_ip = "54.12.34.56"
```

Copy that IP — you need it for Chapter 10 and 11.

> ⚡ **What just happened?** You described infrastructure in a text file and Terraform created it in AWS, in the right order, handling all dependencies. The `terraform.tfstate` file now records what exists. Terraform uses this state to calculate future diffs. **Never manually edit the state file** — Terraform owns it.

> 💡 **`terraform destroy`:** Run this when you're done (or when your free tier expires) to delete everything Terraform created — cleanly, in the right order, with one command.

```bash
# Add terraform directory (but NOT .terraform/ or state files)
echo ".terraform/" >> ../.gitignore
echo "terraform.tfstate*" >> ../.gitignore
git add terraform/main.tf ../.gitignore
git commit -m "terraform: add infrastructure config for EC2 deployment"
```

````

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add chapter 9 - terraform"
```

---

## Task 15: README — Chapter 10 (Deploy to EC2)

**Files:**
- Modify: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md` (append)

- [ ] **Step 1: Append Chapter 10**

````markdown
---

## Chapter 10: Deploy to EC2 — Your CV on a Real Server

You have an EC2 instance running. Now SSH in, install Docker, and run your container.

### 10.1 Connect via SSH

```bash
ssh -i ~/.ssh/id_ed25519 ec2-user@<YOUR_SERVER_IP>
```

**What this does:**
- `ssh` — Secure Shell. Opens an encrypted terminal session to a remote machine.
- `-i ~/.ssh/id_ed25519` — use your private key for authentication (the public key is already on the server via Terraform)
- `ec2-user` — the default username on Amazon Linux
- `<YOUR_SERVER_IP>` — the Elastic IP from `terraform output`

You'll see a prompt like `[ec2-user@ip-172-31-xx-xx ~]$` — you're now inside the remote server.

> ⚡ **What just happened?** Your Mac used your private SSH key to prove its identity to the server (the server already has your public key from Terraform). The connection is encrypted. You're typing into a terminal running on a computer in an AWS data centre in Ireland.

### 10.2 Install Docker on the EC2 Instance

```bash
# All of these run ON the EC2 server
sudo yum update -y
sudo yum install -y docker
sudo systemctl start docker
sudo systemctl enable docker        # Start Docker automatically on reboot
sudo usermod -aG docker ec2-user    # Allow ec2-user to run docker without sudo
```

Exit and reconnect for the group change to take effect:
```bash
exit
ssh -i ~/.ssh/id_ed25519 ec2-user@<YOUR_SERVER_IP>
docker --version   # Should work without sudo now
```

### 10.3 Get Your CV Files onto the Server

You have two options. Use Option A (clone from GitHub — simpler):

**Option A: Clone from GitHub**
```bash
git clone git@github.com:ryanfreiha/ryan-cv.git
cd ryan-cv
```

If SSH doesn't work on the server, use HTTPS:
```bash
git clone https://github.com/ryanfreiha/ryan-cv.git
cd ryan-cv
```

**Option B: Copy files from your Mac (if repo is private)**
```bash
# Run this on your Mac (not the server)
scp -i ~/.ssh/id_ed25519 -r /path/to/ryan-cv ec2-user@<SERVER_IP>:~/ryan-cv
```

`scp` = Secure Copy — works like `cp` but over SSH.

### 10.4 Build and Run the Container

```bash
# On the EC2 server, inside the ryan-cv directory:
docker build -t ryan-cv .
docker run -d -p 80:80 --name ryan-cv-server ryan-cv
docker ps   # Confirm it's running
```

Visit `http://<YOUR_SERVER_IP>` in your browser — your CV, served by nginx inside Docker on an EC2 instance in AWS.

> ⚡ **What just happened?** A real computer in an AWS data centre is running your Docker container. nginx inside the container is listening on port 80. The Security Group Terraform created allows inbound traffic on port 80. Anyone in the world can visit that IP and see your CV.

### 10.5 Make Future Deployments Easier

Create a deploy script on the server. Create `~/deploy.sh`:

```bash
#!/bin/bash
set -e   # Exit immediately if any command fails

echo "Pulling latest code..."
cd ~/ryan-cv
git pull origin main

echo "Building new image..."
docker build -t ryan-cv .

echo "Stopping old container..."
docker stop ryan-cv-server || true
docker rm ryan-cv-server || true

echo "Starting new container..."
docker run -d -p 80:80 --name ryan-cv-server ryan-cv

echo "✅ Deployed successfully"
```

```bash
chmod +x ~/deploy.sh
```

Now deploying is just: `./deploy.sh`.

````

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add chapter 10 - deploy to ec2"
```

---

## Task 16: README — Chapters 11 & 12 (DNS Migration + Kubernetes Overview)

**Files:**
- Modify: `C:/Users/Ghadi/IdeaProjects/ryan-cv-guide/README.md` (append)

- [ ] **Step 1: Append Chapters 11 and 12**

````markdown
---

## Chapter 11: Point the Domain to AWS — Live Traffic Migration

Your CV is now running on EC2. Let's move `ryan.freiha.dev` from GitHub Pages to your EC2 server.

### 11.1 Update the DNS Record

1. Log in to [cloudflare.com](https://cloudflare.com) → `freiha.dev` zone
2. Find the `ryan` record you created in Chapter 3 (currently CNAME → `ryanfreiha.github.io`)
3. **Delete** the old CNAME record
4. **Add a new record:**
   - **Type:** `A`
   - **Name:** `ryan`
   - **IPv4 address:** `<YOUR_ELASTIC_IP>` (from `terraform output`)
   - **Proxy status:** ☁️ **Proxied** (orange cloud ON this time)
   - **TTL:** Auto

> 💡 **Why proxied now?** In Chapter 3, we needed DNS only so GitHub could verify the domain. Now you control the server — enabling Cloudflare's proxy adds HTTPS (via Cloudflare's certificate, no Let's Encrypt needed), DDoS protection, and caching in front of your EC2 instance. Your server's real IP is hidden behind Cloudflare.

### 11.2 Watch the Migration

```bash
# Run repeatedly — watch the DNS record change
watch -n 5 "dig ryan.freiha.dev +short"
```

When the old TTL (Time To Live) expires globally, `dig` will start returning Cloudflare's proxy IPs instead of GitHub's IPs.

> ⚡ **What just happened?** You migrated a live website from one hosting provider to another with zero downtime. During propagation, old DNS caches still pointed to GitHub Pages — visitors got the old server. As TTL expired cache-by-cache around the world, traffic gradually moved to your EC2 instance. This is how real migrations work.

### 11.3 Verify

```bash
curl -I https://ryan.freiha.dev
```

Look for:
```
server: cloudflare
```

Cloudflare is now the edge — it terminates HTTPS, caches your content, and forwards requests to your EC2 server on port 80.

Visit `https://ryan.freiha.dev` — your CV, your domain, your server, your container.

---

## Chapter 12: Kubernetes — Light Overview (Optional)

You now have one Docker container on one EC2 server. What happens when:
- The server crashes?
- You need to update the container with zero downtime?
- You need 10 containers to handle traffic?

That's the problem Kubernetes (k8s) solves.

> 💡 **Kubernetes is a container orchestrator.** It manages a cluster of servers and decides where to run containers, restarts them if they crash, scales them up and down, and routes traffic between them.

### 12.1 Architecture

```
Control Plane (the brain)          Worker Nodes (where containers run)
┌─────────────────────────┐       ┌──────────────┐ ┌──────────────┐
│ API Server              │       │ kubelet       │ │ kubelet       │
│ (everything talks here) │──────▶│ (runs pods)   │ │ (runs pods)   │
│ Scheduler               │       ├──────────────┤ ├──────────────┤
│ (decides which node)    │       │ Pod: nginx   │ │ Pod: nginx   │
│ etcd                    │       │ Pod: nginx   │ │              │
│ (cluster state DB)      │       └──────────────┘ └──────────────┘
└─────────────────────────┘
```

### 12.2 Key Concepts

| Concept | What it is |
|---------|-----------|
| **Pod** | Smallest deployable unit — one or more containers that share a network |
| **Deployment** | Declares desired state: "always run 3 replicas of this pod" |
| **Service** | A stable network endpoint in front of pods (pods come and go, Service IP stays) |
| **Node** | A physical or virtual machine in the cluster |
| **kubectl** | The CLI for interacting with a k8s cluster |

### 12.3 What a Deployment Looks Like

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ryan-cv
spec:
  replicas: 3          # Always keep 3 copies running
  selector:
    matchLabels:
      app: ryan-cv
  template:
    metadata:
      labels:
        app: ryan-cv
    spec:
      containers:
      - name: nginx
        image: ryan-cv:latest
        ports:
        - containerPort: 80
```

If one pod crashes, Kubernetes notices (it's no longer "3 running") and starts a replacement immediately. If you update the image, it rolls out the new version pod-by-pod with no downtime.

### 12.4 Try it Locally (optional)

```bash
brew install minikube kubectl
minikube start
kubectl get nodes         # See your local "cluster" (one node)
kubectl apply -f deployment.yaml
kubectl get pods          # See your 3 pods running
kubectl get services
```

> 💡 **When do you need Kubernetes?** When you have many containers, need automatic recovery from failures, need zero-downtime deployments, or need to scale horizontally under load. For a CV — you don't. But for a production API handling millions of requests — absolutely.

---

## What You've Built

| Technology | What you did |
|-----------|-------------|
| Git | Tracked every change, committed history, pushed to GitHub |
| GitHub Pages | Hosted the CV for free as a static site |
| DNS + Cloudflare | Configured `ryan.freiha.dev` with CNAME and A records, used Cloudflare proxy |
| Bash & Linux | Navigated servers, piped commands, read logs, managed files |
| Networking | Traced DNS → TCP → TLS → HTTP for a real request |
| GitHub Actions | Automated validation and deployment on every push |
| Docker | Packaged the CV + nginx into a portable container |
| AWS | Provisioned real cloud infrastructure, used IAM, EC2, Elastic IP |
| Terraform | Described and created infrastructure as code |
| EC2 Deployment | SSH'd into a real server, ran Docker, deployed live |
| DNS Migration | Moved a live site from GitHub Pages to AWS with zero downtime |

You now have the foundation for a career in platform engineering. Every production system you'll ever work on uses some combination of these tools.

````

- [ ] **Step 2: Final commit**

```bash
git add README.md
git commit -m "docs: add chapters 11 and 12 - dns migration and kubernetes overview"
```

- [ ] **Step 3: Verify the complete README renders correctly**

Push to GitHub and view the README on GitHub.com — verify all sections render, code blocks are formatted, table of contents links work (click each one).

```bash
git push
```

---

## Self-Review Checks

- [ ] All 12 chapters present in README (0 through 12, Chapter 0 counts as prerequisites)
- [ ] `index.html` includes all sections: about, skills, experience, education, contact
- [ ] Dark mode toggle in `script.js` uses `localStorage` for persistence
- [ ] Dockerfile uses `nginx:alpine` and COPYs to the correct nginx path
- [ ] Terraform config includes `aws_eip` resource and `output "server_ip"`
- [ ] `.gitignore` entries cover `.terraform/` and `terraform.tfstate*`
- [ ] GitHub Actions workflow has `needs: validate` on the deploy job
- [ ] Chapter 3 explicitly says to use **DNS only** (not proxied) for GitHub Pages
- [ ] Chapter 11 explicitly says to switch to **proxied** for EC2
- [ ] Cost table present showing free tier / ~$9/mo estimate
