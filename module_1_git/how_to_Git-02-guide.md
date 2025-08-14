# Module 2 – Let's Git 🤓 Part 2


## This note covers the exercise on the day 2 and day 3 after the setup 

##  System
Description:	Kubuntu-T2 24.04.2 LTS
Release:	24.04
Codename:	noble

---
## Important Concepts: 
1. Use 'git status', 'git log', 'git remote -v', 'git branch -v' to check the status often
2. git can only track the file, not folder  

---
## 1. Create a Local Git Repo and Link It to GitHub (Day 2)
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

---
## 2. Fork a Git Repo from GitHub and Sync to a Local Folder (Day 2)
Just follow this guide and/or watch the vidoe
- [UofT DSI Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#setting-up)
- [How to Fork a Repository](https://youtu.be/H-8kzcQWJ7U)
- [How to Submit an Assignment](https://youtu.be/gXtxb0ECs2A)


To clone your forked repo into a local folder:

```bash
git clone [repository_url]               # Clone an existing repository
git clone [repository_url] [new_dir]     # Clone and rename the directory
```

---
## 3. Restore a document from other GitHub Repo (Day 3)
### Background
Someone accidentally delete the avocado from the guacamole recipe, let's fix it. 

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
git switch -c fix-avocados e4912279bfddcc05c9c91924cd40efcf04f2f1c3   # create a new branch 'fix-avocados' to restore the document to its previous time point

# commit id = e4912279bfddcc05c9c91924cd40efcf04f2f1c3
# Use'git log' to retrieve commit id. 

git status

## Fork the dsi_guacamole to your own Git Repo
git remote -v 
git remote rename origin upstream # rename origin to upstream 
git remote add origin https://github.com/yikai82/dsi_guacamole.git  # add new origin 
git remote -v
```

The terminal should have the correct output as below. You will have upstream (point the dtxe) and origin (on your own github):
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

---
## 4. Merge/Pull other document from Git Repo (Day 3)
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
# I am no sure which one I was using...' '
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

---
## 5. Cohort7 ---not complete yet
### Background
The instructor was simulating a chaos situation where multiple people working on the same document in an industry setting. 

```bash
## clone the cohort7 playground
git clone https://github.com/simeon-demo/cohort7_playground.git
cd cohort7_playground

## waiting for the invitation as collaborator while you can edit the file you like
ls 
git status; git remove -v
git switch -c [branch.name]
code README.md  # just open and edit whatever you like
git add README.md; git commit

## once you have accepted the invitaion as collaborator, you can start push the change
git push # This will push the local branch along with the edit to the github 
git push README.md upstream main # it might no longer work as if the branch was locked
git pull --no-rebase # to solve any conflict if there is any 
git branch -vv
 
```
### I am totally lost here so... 🚧 🚧 🚧


---
## Situation Room 🚨

### Situation 1: You mess around a local folder that is tracked by git on GitHub and you desperately want to reset every thing on your local machine. For example, You have a repo on GitHub that is synced with a local folder. You made a mistake, and now the local folder and the repo on GitHub are no longer in sync because of a conflict. You want to preserve the repo that is on GitHub.  

Possible triggers: 
(1) Delete a folder (containing files) on a GitHub repo, and you modified the same file in the local. Now, the GitHub repo it is gone, the local repo says you need to commit and push a change, which you have no place to push. 

**Solution:** Since you want to preserve the GitHub Repo. Remove (or be safer, just rename) the local repo to a different name (ex, my repo -> my_repo_delete) and re-clone the repo from GitHub using:

```bash
git clone [url] 
```
It will create a new 'my repo" and everything is **reset**. 

--
### Situation 2: You cloned of someone's repo on GitHub and created a local repo. Then, you also editted a document. You learned that there are new updates from the upstream so you decide to pull. Now you've got an error:

```bash
Updating 09ffdf8..6fa9163
error: Your local changes to the following files would be overwritten by merge:
        02_activities/assignments/assignment.sh
Please commit your changes or stash them before you merge.
Aborting
```

Possible trigger: You work on the file xxxxx.xx and the upstream has a new dataset uploaded. It also have an older version of file.py.
You already edit the older version of file.py. If you pull, you risk overwriting your editted file

**Solution: (1) Stash local work, (2) Pull from GitHub, (3) Reapply local changes**

```bash
cd ./path/to/your/work/directory
git status                # Check current changes
git remote -v             # View origin and upstream paths
git stash                 # Save local changes
# Check your current branch
git switch main           # Switch to main branch if pushing to main
git switch <branch-name>  # Switch to target branch, if not main
git pull origin main      # Pull changes from GitHub
git stash list            # View saved stashes
git stash pop             # Reapply stashed changes
```

--
### Situation 3: You forked the DSI/sql already and also created a branch assignment on GitHub. Then you created a local repo (/path/to/work/sql). From GitHub, you know that both your main branch and assignment branch have new updates. You want the new updates to apply to your local repo and the assignment branch. You want to update everything using the terminal 

**Solution:**

```bash
cd path/to/work/directory/sql
git status                      # it should point to the assignment branch 
git remote -v                   # check the remote setting
git remote add upstream [url]   # set up the upstream
git log [branch/name]           # if no branch name is given, it will output you current head 
git log upstream/main           # upstream/main is where I assigned for the UofT-DSI/sql 
git log assignment..upstream/main  # this will show if there is any different, if it is return empty, you should be good. 
## If there is difference 
git fetch upstream main
git pull upstream main          # you will see conflict message
git pull --no-rebase upstream main # this will download the update to you local repo
git push                        # this will push update to your repo assignment on GitHub 
```

Share my git log ouput: 

```bash
$ git log
commit c6866b50a78e96433e0079be51356372639bc74a (HEAD -> assignment, origin/assignment)
Merge: 084a71f 47bbd0b
Author: yikai82 <yikai.su89@gmail.com>
Date:   Wed Aug 6 23:06:57 2025 -0400

    Merge branch 'main' of https://github.com/UofT-DSI/sql into assignment

commit 47bbd0b190d5b60ef1f185c2826f3f2e6af787fa (upstream/main)
Merge: e95bd72 b5eb495
Author: CODE, POTATO <t.rose.github@protonmail.com>
Date:   Wed Aug 6 21:43:40 2025 -0400

    Merge branch 'main' of https://github.com/UofT-DSI/sql

commit e95bd72edc7f836762c7c34b2a5776c6a781a7e2
Author: CODE, POTATO <t.rose.github@protonmail.com>
Date:   Wed Aug 6 21:43:34 2025 -0400

    in class code for session 2!

commit 084a71fa2661ef83432ee708fae16928b626b4ef
Merge: 2fc3737 b5eb495
Author: yikai82 <yikai.su89@gmail.com>
Date:   Wed Aug 6 18:14:27 2025 -0400

    Merge branch 'main' of https://github.com/UofT-DSI/sql into assignment


```
### Later, you learn that the branch name 'assignment' needs to be renamed to assignment-one

**Solution:** Rename the oen on the GitHub, and then update the local repo

```bash
git status # check your HEAD
git switch [branch.name]  # move HEAD to branch assignment 
git branch -m assignment-one # if you are on branch assignment
# if you are on a differenet branch
git branch -m assignment assignment-one

``` 

--
### Situation 4: You create a clone of with the name 'FUN', and now you want to rename it to 'fun". The Repo FUN also has a local repo 'fun'. The rename is case-senstive and you worry it might trigger errors later 

**Solution: (1)Switch to a different branch temporarily, (2)Rename the branch 'Fun' to [temp-branch], (3) Rename [temp-branch] to 'fun, (4)Delete the old branch 'FUN'**

```bash
git branch -m FUN temp-branch       # Rename to something else temporarily
git branch -m temp-branch fun       # Then rename to final lowercase name
git push origin -u assignment       # Push the new branch to remote and set it to track origin
git push origin --delete FUN        # Delete the old branch from the remote (optional but recommended):
```

### Situation 5: You want to pull a remote branch to the local repo that you've setup already. This is a case similar to the big-batch. However, you are also confused about how many branches you have locally or remotely

**Solution:**

```bash
git clone [url] # Clone an online GitHub repo to local, the local repo is likely called 'main'
                # From GitHub, you know it has a separate branch 'new-branch 
git pull [origin]/[upstream] [branch.name]  # Depending on the setting, need to define if origin or upstream 
git pull origin -u [branch.name]        # Push the new branch to remote and set it to track origin:
git branch -d [local_branch_name]       # delete unwanted branch      
git branch -v                           # check local branchs
git branch -vv                          # check local branch + more details 
git branch -r                           # check remote branch
git branch -rv                          # check remote branch + more details
```

---
### Situation 6: Reset the HEAD to the previous time point
Strigger: You edit a script and realize nothing work so you just want to revert the file to the previous stage (i.e., like the version control in microsoft word or excel)
**Note: The hard reset will erase everything including the commit commend**  
**Solution:**

```bash
git status
git log                     # to retrieve the commit# 
git branch -vv              # make sure you are in the current branch
git reset --hard [commit#]  # reset HEAD
git push force              # force the change to the GitHub
```

---
### Situation 7: How to remove an unwanted branch repo on GitHub and local repo




---
### ✅ Proper Way to Switch and Track a Remote Branch

```bash
git fetch origin
git switch [branch-name]
git branch --set-upstream-to=origin/[branch-name]
git push -u origin [branch-name]
```




---
### 📚 Other References:
1. [U of T DSI GitHub Cheatsheet](https://github.com/UofT-DSI/git/blob/main/01_materials/git_cheatsheet.md)