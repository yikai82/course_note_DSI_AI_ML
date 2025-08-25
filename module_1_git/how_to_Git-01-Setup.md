<p align="center">
  <img src="https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png" alt="Git Logo" width="120">
</p>

#
<h1 align="center">Module 1 – How to Git - Part 1 🤓 </h1>

<p align="center">
  🚀 Let's Get Ready (Day 1)<br>
  <a href="#key-note-and-important-concept">Key Notes</a> •
  <a href="#situation-room-" style="background-color:#9c4965; color:white; padding:0px 9px; border-radius:4px; font-weight:regular; text-decoration:none;">Situation Room</a> 
  <!-- <a href="#other-references">References</a> -->
</p>

## System
<a href="" style="background-color:616161; color:white; padding:0px 9px; border-radius:4px; font-weight:bold; text-decoration:none;">Linux</a>  Kubuntu-T2 24.04.2 LTS  
Release:	24.04  
Codename:  <a href="" style="background-color:1B89D0; color:white; padding:0px 9px; border-radius:4px; font-weight:semi-bold; text-decoration:none;">noble</a>  
Kernel Version: Linux 6.14.0-1-t2-noble

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
## Situation Room


