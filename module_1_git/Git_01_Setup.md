<p align="center">
  <img src="https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png" alt="Git Logo" width="120">
</p>

<h1 align="center">Module 1 – How to Git - Part 1 🤓 </h1>

<p align="center">
  🚀 <b> Day 1: Let's Get Ready 🚀 </b><br>
<br>v

## System

<div align="left">
  <div style="margin: 2px 0;">
    <img src="image/Linux2.svg" alt="Linux" width="50" style="vertical-align: middle; margin-right: 6px;">
    <span style="vertical-align: middle;">Kubuntu-T2 24.04.2 LTS</span>
  </div>
  <div style="margin: 2px 0;">
    <img src="image/Noble.svg" alt="Noble" width="50" style="vertical-align: middle; margin-right: 6px;">
    <span style="vertical-align: middle;">Codename: Noble</span>
  </div>
</div>  

Release:	24.04 LTS  
Kernel Version: Linux 6.14.0-1-t2-noble  
Hardware: Intel® Core™ i9-9880H CPU @ 2.30GHz, 16 GM RAM

---

## 1. Setup Git Identity and Credential Manager in Linux

```bash
git-credential-manager --version   # Check to ensure it is installed 
git config --global user.name "<user name>"
git config --global user.email "<user email>"
git config --global core.editor "code --wait"
# Set VS Code as the default editor for Git, so whenever Git needs you to write a commit message or edit a rebase, it will open VS Code instead of the default (like nano or vim).
git config -l  # List the current Git config
git credential-manager github list        # Show list of credential managers
git credential-manager github login       # Login as credential manager

# I added the following two commands:
git config --global credential.credentialStore secretservice
git config --global credential.helper manager
```

### Let me explain why I add the last two commands for my Linux
> After successfully login and running `git credential-manager github list`, I see the following error:
>
> ```bash
> **fatal: No credential store has been selected.**
> Set the GCM_CREDENTIAL_STORE environment variable or the credential.credentialStore Git configuration setting to one of the following options:
>
> secretservice : freedesktop.org Secret Service (requires graphical interface)
> gpg           : GNU pass compatible credential storage (requires GPG and pass)
> cache         : Git's in-memory credential cache
> plaintext     : store credentials in plain-text files (UNSECURE)
>
> See https://aka.ms/gcm/credstores for more information.
> ```

**To fix this:**

```bash
git config --global credential.credentialStore secretservice
# If to unset
git config --global --unset credential.credentialStore
```

**Recheck the config:**

```bash
git config -l
user.name=<github.name>
user.email=<github.login.email.com>
core.editor=code --wait
credential.credentialstore=secretservice
```

> ⚠️ **Authentication Error when running `git push`:**  
> Later, when I tried to run `git push` (after `git add` and `git commit`), I got another issue — a system window popped up asking for GitHub credentials:
>
> ```bash
> git push -u origin main
> error: unable to read askpass response from '/usr/bin/ksshaskpass'
> Username for 'https://github.com': abcdef12345
> remote: Invalid username or token. Password authentication is not supported for Git operations.
> fatal: Authentication failed for 'https://github.com/yikai82/test_repo.git/'
> ```

My guess is that this is a Git authentication issue with the KDE environment — possibly caused by `ksshaskpass` conflicting with Git credential handling.

To resolve:

  ```bash
  git config --global credential.helper manager
  ```

> This tells Git to use Git Credential Manager (GCM), a cross-platform tool maintained by Microsoft.  
> It manages credentials by delegating to a backend credential store, which must also be configured.


### 🔑 Credential Summary:

  - `credential.helper=manager`  
  Uses Git Credential Manager (GCM). Required for managing login sessions with GitHub or other providers.

  - `credential.credentialStore=secretservice`  
  Specifies the backend GCM uses for storing credentials (compatible with GNOME Keyring / KDE Wallet).

---

### .gitignore

  - It tells Git which files and folders to leave untracked — won't be staged committed or pushed

  - 📌 .gitignore **only works on untracked** files. If you already committed a file, adding it to .gitignore won't remove it. You'd need to untrack it first:

    ```bash
    git rm --cached <filename>
    ```  
    
  - GitHub maintains a handy collection of ready-made .gitignore templates for common languages and frameworks [here](github.com/github/gitignore).     

  - Key rules: 
      - `*`matches anything within a single directory level
      - `**` matches across directory levels (e.g. `**/*.log`)
/ at the start anchors to the repo root (e.g. /dist only ignores the top-level dist/)
! negates a pattern (un-ignores something previously ignored)
Lines starting with # are comments

      - `.gitignore` only works on untracked files. If you already committed a file, adding it to .gitignore won't remove it. You'd need to untrack it first:

  - Template  

  ```gitignore
  # Ignore a specific file
  secret.env
  
  # Ignore a folder
  node_modules/

  # Ignore all .log files
  *.log

  # Ignore all .txt files except one
  *.txt
  !important.txt

  # Ignore files in a specific folder
  build/*.js

  # Ignore a directory and everything inside it
  draft_note/
  cache/

  # Ignore a directory anywhere is the repo
  **/draft_note/
  ```

  ```bash
  repo/
  ├── .gitignore
  ├── draft_note/    # <--- /draft_note/ 
  ├── notes/
  │   └── draft_note/  # <--- /note/draft_note/ 
  └── test.txt
  ```
  
  ⚠️  
  
  - Use `folder_name/` to a signle folder at any depth
  - Use `**/folder_name/` if expect multiple locations




