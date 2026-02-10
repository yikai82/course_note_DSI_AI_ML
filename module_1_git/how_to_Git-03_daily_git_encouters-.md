<p align="center">
  <img src="https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png" alt="Git Logo" width="120">
</p>
<h1 align="center">
  Git Daily Encounters <br>
  ♻️ ⚙️ 🔨 = 🤓 </h1>


<!-- <p align="center">   
  <a href="#-references">References</a>
</p> -->

## Key Notes and Important Concepts

> [!NOTE]  
> 1. This is a collection of git script (cleaner) that I use daily. For basic information, Check 👉[how_to_Git-02-guide_ver02](/module_1_git/how_to_Git-02-guide_ver02.md)  
> 
> 2. **`git add .`**: Stages everything that changes (including new files, untracked files) in the current folder and its subdirectories.  
> 
> 3. **`git add -u`**/**`git add --update`**: Stages modified and deleted files (already tracked).  
> 
> 4. `git restore --staged file_name` to undo the previous staging, but it’s not required just to update the staged snapshot.


[↥ back to top](#content)&emsp;|&emsp;[Return Main Page 🏠](/README.md) </sub> 

---
> [!IMPORTANT]
> 1. When creating a fresh local repo using `git clone [url]`, it creates a local branch (usually "main" or whatever the default branch of the repo is), and is **automatically** set to track the remote branch (origin/main).  
> 💡**Note**: The automatic tracking only applies to the branch at clone time (usually main). A later local branch created with `git switch -c new-branch`, won’t be tracked until explicitly push them the first time with `git push -u origin new-branch`.  
>
> 2. Only git log is using **syntax [repo_name/branch]**; other git function will use repo_name branch.  For example: `git log upstream/main` vs. `git push origin main`  
>
> 3. `git add` takes a snapshot to capture the file at that *exact moment*. Further changes on the same file **won't be captured** unless you apply `git add` again.  
> 
> 4. When starting with a local repository and linking it to GitHub, at least one commit must be created and pushed to GitHub to establish the link.
>
> 
> 

[↥ back to top](#content)&emsp;|&emsp;[Return Main Page 🏠](/README.md) </sub> 

---
> [!WARNING]  
> 1. Don’t confuse your **local repo** with your **remote repo** on GitHub. They are two separate worlds.  
> <p align="center">
>   <img src="image/Dragon.png" alt="dragon" width="90">  
>   &nbsp;&nbsp;&nbsp;
>   <span style="font-size: 2.5em; font-weight: bold;">VS</span>  
>   &nbsp;&nbsp;&nbsp;
>   <img src="image/Wall-E-Wall-E.512.png" alt="robot" width="90">
> </p>  
> 
> 2. `git add -u` vs. `git push -u`: both have **`-u`**, but **`-u`** has different meanings  
> 
>    | Command       | `-u` means   | Purpose                                                              | What it affects                | 
>    | ------------- | ------------ | -------------------------------------------------------------------- | ------------------------------ | 
>    | `git add -u`  | **update**   | Stages changes to **tracked files only** (modifications + deletions) | Working tree → Staging (index) | 
>    | `git push -u` | **upstream** | Pushes commits and sets the default remote tracking branch           | Local repo → Remote repo       |
> 
> 
> 
> 
<sub>[↥ back to top](#content)&emsp;|&emsp;[Return Main Page 🏠](/README.md) </sub>  

---
![BONUS](image/BONUS.svg)  

1. **`git checkout`** Temporarily look at the specific commit ----> Good for inspection or temporary testing

<br>   

<p><i><b>Disclaimer</b>: I have made every effort to ensure the accuracy of this document, but errors may still be present. Please proceed with caution. </i></p>

---
<!-- ## Content -->



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

<sub>[↥ back to top](#content)&emsp;|&emsp;[Return Main Page 🏠](/README.md) </sub>  

---
### Case 1 - Clone from GitHub

**Requirement**: Repo in your own GitHub or you have permission to work with

```bash
git clone [repository_url]          # clone an existing repository
git branch -vv                      
# should return: **main 717a400 [origin/main]** indicating that the local branch is automatically set to track the remote branch (origin/main).

git remote -v                       # check the remote setting
git remote add upstream [url]       # set up the upstream


## >>>>>> if want to check/fetch update from the upstream <<<<<< ## 
git fetch upstream main
git log origin                      # if no branch name is given, it will output you current HEAD 
git log upstream/main               # upstream/main is where I assigned for the UofT-DSI/sql, 
                                    # need to fetch first to generate log
git log assignment..upstream/main   # this will show if there is any different,
```

<sub>[↥ back to top](#content)&emsp;|&emsp;[Return Main Page 🏠](/README.md) </sub>  

---
### Case 2 - Start with a local repo (a folder), initiate git and sync with Github

1. Create a Local Git Repo `test_repo` and Link It to GitHub: 

    ```bash
    cd path to work  # path to work directory
    mkdir test_repo
    cd test_repo
    git init -b main  # Initialize as the default branch with name 'main'
    ```

2. Go to: GitHub > New Repository > name: test_repo
   - ⚠️ **Do NOT initialize with README, NO .gitignore, no license. (Keep it empty so your push won’t conflict.)**

3. Create a single file, commit, push it to link the local repo to GitHub: 

    ```bash
    touch README.md
    git add .
    git commit -m "Initial commit"
    git remote add origin <url>
    git push -u origin main # set up upstream : git push -u <remote> <branch>
    ```

<sub>[↥ back to top](#content)&emsp;|&emsp;[Return Main Page 🏠](/README.md) </sub> 

---
### Case 3 - Create a local branch and set up the upstream

**Requirement**:  
(1) Repo in your own GitHub or you have permission to work with.   
(2) pre-existinh local repo.

```bash
cd /path/to/folder
git remote -vv    # chcek tthe current setting
git switch -c [branch.name]
git push -u origin [branch.name]  # -u: set upstream; push local branch and track it on GitHub
git remote -vv    # confirm the setting is updated
```
⚠️ **Note:**  
You’d only need `-u` again only if: 
- You’re pushing a brand-new branch for the first time, or
- You deleted and recreated the branch upstream.


<sub>[↥ back to top](#content)&emsp;|&emsp;[Return Main Page 🏠](/README.md) </sub>  

---
### Case 4 - Deal with divergent between local and remote branches with multiple files are overwritten  

**Purpose/Situation**: 
1. You (auto) merged remote branch A and remote branch B on GitHub. 
2. Branch B was 28 commits ahead of branch A. 
3. You added more change to the branch A, and try to push. You got an error:   

⚠️ **error 1**: 
```bash
<br$ git push
To https://github.com/yikai82/repo_name.git
 ! [rejected]        backbone -> backbone (fetch first)
error: failed to push some refs to 'https://github.com/yikai82/.git'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. This is usually caused by another repository pushing to
hint: the same ref. If you want to integrate the remote changes, use
hint: 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
4. You than do a `git pull`, and using git status, you found another message:  

⚠️ **error 2**:
```bash
$ git status
On branch backbone
Your branch and 'origin/backbone' have diverged,
and have 1 and 28 different commits each, respectively.
```

5. You notice that a lot of important files on the local branch A have been overwritten. Since Branch A and Branch B have different goal, they should never have been merged 

👉 **Solution**: Find the last good commit and reset everything on local Branch A and then push to remote branch A 
```bash
git log local_branch origin/remote_branch
git reset --hard commit_sha # the first 8 digits of the sha ceb20bb
git push --force-with-lease origin backbone # overwrite local to the origin/remote
```


---
More to come....🔨 🔧 🛠️ 



<!-- ---
### 5. Delete or Scarp the unwanted GitHub Repo
some text here

```bash 
# some code...
```

---
### 6. Remove files/folder from Git tracking 

✅ Key takeaway: Always remove from Git tracking first (git rm --cached) before relying on .gitignore.



some text here

```bash
# some code...
```


---
### 7. Create a Local Git Repo and Link It to GitHub (Day 2)  
To create a local repo called `test_repo` and linking it to GitHub during the day 2 git in-class exercise: 

```bash
cd path to work            # path to work directory
mkdir test_repo
cd test_repo
git init -b main              # Initialize with main as the default branch
touch test.txt; code test.txt # Create test.txt and open it in VS Code
git status
git add test.txt
git status
git log
git commit
git remote add origin https://github.com/yikai82/test_repo.git
git status
git remote -v
```

<sub>[↥ back to top](#)</sub>

---
### 8. Restore a document from other GitHub Repo (Day 3)

### Background
Someone accidentally delete the avocado from the guacamole recipe, let's fix it. 

📌 **main concept:**  
1. How to create a local branch and push to GitHub in shell. 
2. Restore 

Follow the command below to create a situation:  

```bash 
cd ~/path/to/work/directory # your work directory
git clone https://github.com/dtxe/dsi_guacamole.git # this will create a folder named 'git_gaucamole' under your working directory
cd ./dsi_guacamole.git
git status
git log # you will see two logs and one of them have a comment "Accidentally delete avocados"
ls # list the file
code guacamole.md 

## Here you will see that avocados was deleted by accident so we want to restore
git switch -c fix-avocados e4912279bfddcc05c9c91924cd40efcf04f2f1c3   # create a new branch name 'fix-avocados' to restore the document to its previous time point

# commit id = e4912279bfddcc05c9c91924cd40efcf04f2f1c3
# Use'git log' to retrieve commit id. 

git status

## Fork the dsi_guacamole to your own Git Repo
git remote -v 
git remote rename origin upstream # rename origin to upstream 
git remote add origin https://github.com/yikai82/dsi_guacamole.git  # add new origin 
git remote -v
```

The terminal should have the correct output as below. You will have upstream (point the dtxe) and origin (on your own GitHub):
```bash
origin  https://github.com/yikai82/dsi_guacamole.git (fetch)
origin  https://github.com/yikai82/dsi_guacamole.git (push)
upstream        https://github.com/dtxe/dsi_guacamole.git (fetch)
upstream        https://github.com/dtxe/dsi_guacamole.git (push)
```

Now push the origin to fix-avocados: 
```bash
git push -u origin fix-avocados
git push origin main # if your've forked already, you will have a origin main that you can push if needed
```

Open code to edit the guacamole.md to remove `spicy jalapeno pepper or whatever you want to edit`:
```bash
code guacamole.md
git add guacamole.md; git commit
git status; git log                 # to check the status  
git push fix-avocados
```

<sub>[↥ back to top](#)</sub>

---
### 9. Merge/Pull other document from Git Repo (Day 3)
### Background 
This is an example from the day 3 git course when a document needs to be pulled/merged from different source (big batch), and how to troubleshoot. Just follow the command in the previous section to setup upstream.  Follow the command below to create a situation. This  

```bash
git pull upstream big-batch # since upstream is setup properly, you can pull the branch 'big batch' directly

```

You will see a warning message from terminal if you are on mac/linux: 

```bash
From https://github.com/dtxe/dsi_guacamole
 * branch            big-batch  -> FETCH_HEAD
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint: 
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint: 
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
```

Run the following command to merge the conflict document and push:

```bash
# I am not sure which one I was using...' '
git pull --no-rebase upsteram main     
git pull --no-rebase

git status # should indicate there is a conflict 
code guacamole.md  
## You will see your change in the <<<<< HEAD 
## You will see an older change in >>>>>> commit id 
## Click the 'Compare Changes' just on the top of code to see the change
## Accept the change and manually edit what you were planning to do in the 
## previous (i.e., remove spicy)  
git add guacamole.md
git commit 
git push 
```

 -->

---