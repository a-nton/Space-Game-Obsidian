# Obsidian-Git Setup Guide

Free, automatic vault syncing through GitHub. No server, no subscription.  
After setup, you never need to touch a terminal again.

---

## What this does

Everyone on the team gets a copy of the shared vault on their machine. The **obsidian-git** plugin automatically pulls changes when you open Obsidian, and commits + pushes your edits on a timer. Git handles merging. All version history is preserved.

---

## Step 1: Accept the GitHub invite

You should have received an email or GitHub notification inviting you as a collaborator on the vault repo. Accept it. If you don't have a GitHub account yet, create one at [github.com](https://github.com/).

---

## Step 2: Generate a GitHub Personal Access Token

GitHub does not accept passwords for Git operations. You need a token instead.

1. Go to [github.com](https://github.com/) → click your profile picture → **Settings**
2. Scroll down the left sidebar → **Developer settings**
3. **Personal access tokens → Fine-grained tokens → Generate new token**
4. Give it a name like `obsidian-git`
5. Set expiration to whatever you're comfortable with (90 days, or custom)
6. Under **Repository access**, choose **Only select repositories** and pick the vault repo (or choose **All repositories** if you prefer)
7. Under **Repository permissions**, set **Contents** to **Read and write**
8. Click **Generate token**
9. **Copy the token immediately.** You will not be able to see it again. Save it somewhere safe temporarily

---

## Step 3: Install Git and clone the repo

Follow the section for your operating system.

---

### Windows

**Install Git:**

1. Download Git from [git-scm.com/download/win](https://git-scm.com/download/win)
2. Run the installer — **accept all defaults**, just click Next through everything
3. Restart your computer

**Clone the repo:**

1. Open **Git Bash** (search for it in the Start Menu — it was installed with Git)
2. Navigate to where you want the vault to live:

```
cd ~/Documents
```

3. Clone the repo (you'll be given the exact URL):

```
git clone https://github.com/OWNER/REPO-NAME.git
```

4. When prompted for credentials:
    
    - **Username:** your GitHub username
    - **Password:** paste your Personal Access Token (not your GitHub password)
5. Git Credential Manager (included with Git for Windows) stores this automatically. You won't be asked again.
    

Your vault folder now exists at `C:\Users\YourName\Documents\REPO-NAME`.

**If credentials aren't working:**

Make sure credential manager is active:

```
git config --global credential.helper manager
```

Then retry. A browser window or popup should appear for authentication.

To clear a bad stored credential and start fresh:

```
git config --global --unset credential.helper
git config --global credential.helper manager
```

Then retry — it will prompt you again.

---

### macOS

**Install Git:**

1. Open **Terminal** (Cmd+Space, type "Terminal")
2. Type `git --version` and press Enter
3. If Git isn't installed, macOS will prompt you to install Command Line Tools. Click **Install** and wait
4. Run `git --version` again to confirm

**Set up credential storage:**

Before cloning, tell Git to store your token in the macOS keychain:

```
git config --global credential.helper osxkeychain
```

**Clone the repo:**

1. In Terminal, navigate to where you want the vault:

```
cd ~/Documents
```

2. Clone the repo (you'll be given the exact URL):

```
git clone https://github.com/OWNER/REPO-NAME.git
```

3. When prompted:
    
    - **Username:** your GitHub username
    - **Password:** paste your Personal Access Token (not your GitHub password)
4. Your Mac may show a system dialog: **"git-credential-osxkeychain wants to use your confidential information stored in github.com"** — enter your **Mac login password** (the one you use to unlock your computer). This lets the keychain save the token so you aren't asked again.
    

Your vault folder now exists at `/Users/YourName/Documents/REPO-NAME`.

**If credentials aren't working (403 error or authentication failure):**

Your keychain may have a stale credential. Clear it by running:

```
git credential-osxkeychain erase
```

The terminal drops to a blank line waiting for input. Type the following two lines, pressing Enter after each:

```
host=github.com
protocol=https
```

Then press Enter one more time on the empty line to submit. You'll get no confirmation message — this is normal. A `-1` error also just means nothing was stored, which is fine.

Now retry your git operation (`git push` or `git pull`). It will ask for username and token again.

If it still won't prompt you, force Git to ask fresh:

```
git -c credential.helper= push
```

**If you get a 403 even with a valid token:**

Check the remote URL:

```
git remote -v
```

It should show the correct repo URL. If the username or repo name is wrong:

```
git remote set-url origin https://github.com/CORRECT-OWNER/CORRECT-REPO.git
```

---

## Step 4: Open the vault in Obsidian

1. Open Obsidian
2. Click **Open folder as vault**
3. Navigate to the cloned folder (e.g. `Documents/REPO-NAME`)
4. Open it

---

## Step 5: Install the Git plugin

1. In Obsidian, go to **Settings → Community plugins**
2. Turn off **Restricted mode** if prompted
3. Click **Browse** and search for **Git**
4. Find the one by **Vinzent03** (it will just be called "Git")
5. Click **Install**, then **Enable**

---

## Step 6: Configure auto-sync

Go to **Settings → Community plugins → Git** (click the gear icon) and set:

|Setting|Value|
|---|---|
|**Split automatic commit and sync**|OFF|
|**Auto commit-and-sync after the latest commit (minutes)**|`1`|

Leave everything else at defaults. That's it — the plugin will automatically pull, commit, and push every minute while Obsidian is open.

---

## Daily workflow (no terminal needed)

1. **Open Obsidian** — plugin pulls latest changes automatically
2. **Write and edit normally** — plugin commits and pushes every minute
3. **Close Obsidian** — your changes are already synced

You can also manually trigger sync anytime: open the command palette (`Ctrl+P` / `Cmd+P`) and type **Git: Commit-and-sync**.

---

## What if two people edit the same file?

Git merges text files intelligently. If two people edit _different parts_ of the same note, it merges automatically. If two people edit the _exact same line_, Git flags a merge conflict. The plugin will show you both versions and you pick which to keep. With a 1-minute sync interval and a small team, this almost never happens.

**Tip:** Structure the vault so people primarily work in different folders or files. For a game project this is natural — lore in one area, level design notes in another, art references in a third.

---

## Troubleshooting

**"Authentication failed" or 403 error**  
See the credential troubleshooting steps for your OS above. Most likely you need to regenerate your token or clear a stale credential.

**"Merge conflict" notification**  
Open the flagged file. You'll see markers like `<<<<<<< HEAD` and `>>>>>>>`. Keep the version you want, delete the markers, save. Then open the command palette and run **Git: Commit-and-sync**.

**Plugin says "Git is not ready"**  
Git isn't in your system PATH. On Windows, reinstall Git and make sure "Add to PATH" is checked. On macOS, run `xcode-select --install`.

**Large files or images**  
Git works best with text. If your vault includes large images or PDFs, consider adding a `.gitignore` file. For game assets, keep those in your Godot repo, not the lore vault.