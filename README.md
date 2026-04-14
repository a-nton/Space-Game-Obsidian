# Obsidian-Git Setup Guide

Free, automatic vault syncing through GitHub. No server, no subscription.  
After setup, you never need to touch a terminal again.

---

## What this does

Everyone on the team gets a copy of the shared vault on their machine. The **obsidian-git** plugin automatically pulls changes when you open Obsidian, commits your edits every few minutes, and pushes them when you're done. Git handles merging. All version history is preserved.

---

## Part 1: One person creates the shared repo

Only **one person** does this (ideally the vault owner).

1. Go to [github.com](https://github.com) and sign in (or create an account)
2. Click the **+** in the top right → **New repository**
3. Name it something like `game-lore-vault`
4. Set it to **Private**
5. Check **Add a README file**
6. Click **Create repository**
7. Go to **Settings → Collaborators → Add people** and invite each teammate by GitHub username or email

Each teammate accepts the invite via email or GitHub notifications.

---

## Part 2: Install Git (one-time)

### Windows

1. Download Git from [git-scm.com/download/win](https://git-scm.com/download/win)
2. Run the installer. **Accept all defaults** — just click Next through everything
3. Restart your computer

### macOS

1. Open **Terminal** (search for it in Spotlight)
2. Type `git --version` and press Enter
3. If Git isn't installed, macOS will prompt you to install Command Line Tools. Click **Install** and wait

---

## Part 3: Clone the repo (one-time, requires terminal)

This is the only time you touch a terminal.

### Windows

1. Open **Git Bash** (it was installed with Git — search for it in Start Menu)
2. Type the following, replacing the URL with your repo:

```
cd ~/Documents
git clone https://github.com/YOUR-USERNAME/game-lore-vault.git
```

3. A browser window or popup will ask you to sign in to GitHub. Do so.
4. The vault folder now exists at `C:\Users\YourName\Documents\game-lore-vault`

### macOS

1. Open **Terminal**
2. Type:

```
cd ~/Documents
git clone https://github.com/YOUR-USERNAME/game-lore-vault.git
```

3. If prompted for credentials, a browser window will open for GitHub sign-in.
4. The vault folder now exists at `/Users/YourName/Documents/game-lore-vault`

> **Note:** If you get a credential error on macOS, run:
> `git credential-osxkeychain` and follow the prompts, or use the HTTPS personal access token method below.

---

## Part 4: Set up credentials (so Git remembers you)

### Windows

Git for Windows includes **Git Credential Manager** by default. After cloning, it should have already asked you to sign in via browser. If it worked, you're done — it remembers your login.

If it didn't work, check that credential manager is active:

```
git config --global credential.helper
```

It should say `manager`. If blank, run:

```
git config --global credential.helper manager
```

### macOS

Git on macOS uses the system keychain. After cloning and authenticating, credentials are stored automatically.

If you have issues, you can use a **Personal Access Token** instead:

1. On GitHub: **Settings → Developer settings → Personal access tokens → Tokens (classic)**
2. Click **Generate new token (classic)**
3. Give it a name like "obsidian-git"
4. Check the **repo** scope
5. Click **Generate token** and **copy the token immediately** (you won't see it again)
6. When Git asks for your password, paste the token instead of your GitHub password

---

## Part 5: Open the vault in Obsidian

1. Open Obsidian
2. Click **Open folder as vault**
3. Navigate to the cloned folder (`Documents/game-lore-vault`)
4. Open it

---

## Part 6: Install the obsidian-git plugin

1. In Obsidian, go to **Settings → Community plugins**
2. Turn off **Restricted mode** if prompted
3. Click **Browse** and search for **Git**
4. Find the one by **Vinzent03** (it will just be called "Git")
5. Click **Install**, then **Enable**

---

## Part 7: Configure auto-sync

Go to **Settings → Community plugins → Git → Options** and set:

| Setting | Value | Why |
|---------|-------|-----|
| **Vault backup interval (minutes)** | `5` | Auto-commits and pushes every 5 min |
| **Auto pull interval (minutes)** | `5` | Pulls teammate changes every 5 min |
| **Pull updates on startup** | `ON` | Gets latest changes when you open Obsidian |
| **Push on backup** | `ON` | Pushes after every auto-commit |
| **Commit message** | `vault backup: {{date}}` | Keep default or customize |

That's it. Close settings. From now on, the plugin handles everything.

---

## Daily workflow (no terminal)

1. **Open Obsidian** — plugin pulls latest changes automatically
2. **Write and edit** — plugin commits and pushes every 5 minutes
3. **Close Obsidian** — your changes are already synced

You can also manually trigger sync: open the command palette (`Ctrl+P` / `Cmd+P`) and type `Git: Commit-and-sync`.

---

## If someone asks "what if we edit the same file?"

Git merges text files intelligently. If two people edit *different parts* of the same note, it merges cleanly with no intervention. If two people edit the *exact same line*, Git flags a merge conflict. The obsidian-git plugin will show you both versions and let you pick. In practice, with a 5-minute sync interval and a team of five, this almost never happens.

**Tip:** Structure your vault so that people primarily work in different folders or files. For a game project, this is natural — lore in one place, level design notes in another, art references in a third.

---

## Troubleshooting

**"Authentication failed"**  
Re-run the clone step or generate a new Personal Access Token (Part 4).

**"Merge conflict" notification**  
Open the flagged file. You'll see markers like `<<<<<<< HEAD` and `>>>>>>>`. Pick the version you want, delete the markers, save. Then commit-and-sync from the command palette.

**Plugin says "Git is not ready"**  
Git isn't in your system PATH. On Windows, reinstall Git and make sure "Add to PATH" is checked. On macOS, run `xcode-select --install`.

**Large files or images**  
Git works best with text. If your vault includes large images or PDFs, consider adding a `.gitignore` file with entries like `*.psd` or a size threshold. For game assets, keep those in your Godot repo, not the lore vault.

---

## Summary

| | |
|---|---|
| **Cost** | Free (GitHub private repos are free) |
| **Real-time editing** | No (syncs every few minutes) |
| **Version history** | Full history of every change |
| **Terminal needed** | Only once, during initial setup |
| **Server** | None (GitHub handles everything) |
| **Works offline** | Yes (syncs when back online) |
