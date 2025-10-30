# To check the git version:
git --version

# to check the other things:
git help

# if you want to check the full doc for any specific command:
git help pull

# to update the user informations:

git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"

# Update user info for a single repository only:
If you want to change it just for one project, run the same commands without --global inside that repo’s folder:

git config user.name "ProjectUser"
git config user.email "projectuser@example.com"

# Verify current user info:
git config --list


# set different Git user profiles automatically per folder:

setting different Git user profiles (work vs personal)

🧩 Option 1: Per-repository configuration

The simplest method: set a different user.name and user.email inside each repo.

Go to your work project:

cd ~/work/project1
git config user.name "Work Name"
git config user.email "work.email@company.com"


Go to your personal project:

cd ~/personal/project2
git config user.name "Personal Name"
git config user.email "personal.email@gmail.com"


✅ Each repo remembers its own credentials — no overlap.



🧩 Option 2: Automatic switching using Git configuration includes

This is the professional way — perfect if you have many repos.

Step 1: Edit your main global Git config

git config --global includeIf.gitdir:~/work/.path ~/.gitconfig-work
git config --global includeIf.gitdir:~/personal/.path ~/.gitconfig-personal


That means:

Any repo inside ~/work/ will use .gitconfig-work

Any repo inside ~/personal/ will use .gitconfig-personal


Step 2: Create each custom config file

📁 ~/.gitconfig-work
[user]
    name = Work Name
    email = work.email@company.com

📁 ~/.gitconfig-personal
[user]
    name = Personal Name
    email = personal.email@gmail.com


Now Git will automatically switch your identity depending on the folder path — no manual setup per repo!

🧩 Optional: check which config is active

Run this inside any repo:

git config user.name
git config user.email
git config --show-origin user.email


You’ll see which config file it came from (global, local, or included).


# to initialization of any project in a folder:

DevOps> git init
Initialized empty Git repository in C:/Users/mguha/Documents/Git/Git_training/.git/


It will create a hidden file. --> .git


# 🧩 The 3 Main Areas in Git:

Working Directory  →  Staging Area  →  Repository
       (edit)            (add)            (commit)


1️⃣ Working Directory: Where you actually edit files (your local project folder). --> git status

2️⃣ Staging Area (Index): Where you prepare files you want to save in your next commit. --> git add filename

3️⃣ Repository (.git folder): Where Git permanently stores all your committed versions. ---> git commit -m "message"

4️⃣ Remote Repository: The version of your project stored online (shared with teammates)--> git push, git pull, git fetch


Working Directory → Staging Area → Local Repository → Remote Repository


🧠 Summary:

| Step             | Command             | Action                  | Area              |
| ---------------- | ------------------- | ----------------------- | ----------------- |
| Edit files       | *(use your editor)* | Modify code             | Working Directory |---> those are untracked
| Stage changes    | `git add`           | Select files for commit | Staging Area      |---> adding to staging area
| Save snapshot    | `git commit`        | Create permanent record | Local Repository  |---> tracked by git
| Upload to GitHub | `git push`          | Share with others       | Remote Repository |


# So, in short:

3 core areas → Working Directory, Staging Area, Repository

Optional 4th area → Remote Repository (when you use GitHub)


# git add command:

to add any file to the stageing area: 
git add <file name>

to add all file under the project:

git add .

#  git commit command:

git commit → Opens your text editor to write a message.

git commit -m "message" → Commits directly with a short message.

git commit -a -m "message" → Adds and commits all modified tracked files (skips git add).

git commit --amend → Edit the last commit (message or content).


# once we commit any file, after that if we modify that file, and again if we check with git status it will like below:

DevOps> git status

On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   my_1st_file.txt

no changes added to commit (use "git add" and/or "git commit -a")


So, by the git status we can identify the all changes which is done.


# another command to check the chnages: git diff

git diff shows you the differences between files — basically, what has changed in your project.

Think of it like highlighting changes in your homework before submitting it:

Lines you added → show with +

Lines you removed → show with -

It’s a way to check your work before committing.



🧩 4. Other useful options

git diff HEAD → Show all changes (staged and unstaged) compared to last commit

git diff file.txt → Show changes for a specific file

git diff --color-words → Highlight only words that changed instead of full lines


| Command             | What it shows                                             |
| ------------------- | --------------------------------------------------------- |
| `git diff`          | Unstaged changes (working directory vs staging area)      |
| `git diff --staged` | Changes staged for the next commit (staging area vs repo) |
| `git diff HEAD`     | All changes compared to last commit                       |



# git log:

git log shows the history of commits in your repository.

Think of it like a diary of your project — every commit is a “diary entry” that records:

What changed

Who made the change

When the change happened

A unique ID for each commit (SHA)

It helps you track the evolution of your project and see what was done and by whom.

| Part           | Description                                           |
| -------------- | ----------------------------------------------------- |
| `commit <SHA>` | Unique identifier (like a fingerprint) for the commit |
| `Author`       | Who made the commit                                   |
| `Date`         | When the commit was made                              |
| Commit message | Explains what was changed and why                     |


✅ 6. Quick summary:

| Command                   | Purpose                         |
| ------------------------- | ------------------------------- |
| `git log`                 | Show full commit history        |
| `git log --oneline`       | Short version of commit history |
| `git log -p`              | See detailed changes (diffs)    |
| `git log --graph --all`   | Visualize branches and merges   |
| `git log --author="name"` | Filter commits by author        |
| `git log --since="date"`  | Filter commits by date          |



# now creating a repo on th githum and to clone the repo to local system :

git clone -b main https://github.com/manojguha4/Git_traning_2025.git


# Clone into a custom folder name:
git clone https://github.com/username/repository.git my-folder

👉 The repo will be cloned into a folder called my-folder.


# Clone via SSH (if you’ve set up SSH keys):

git clone git@github.com:username/repository.git

👉 SSH is preferred for frequent contributors because it avoids entering your password every time.

# Clone a specific branch:

git clone -b branch-name https://github.com/username/repository.git

👉 This clones only the specified branch.

# Clone a repo with submodules (dependencies):

git clone --recurse-submodules https://github.com/username/repository.git


# Now I have changed the file in remote repo and now I am using the git pull command to update the local repo:

The git pull command is used to update your local repository with the latest changes from a remote repository (like GitHub).


git fetch
git merge


That means git pull first downloads new commits from the remote (fetch), then merges them into your current branch.


# 🧭 Basic Syntax:

git pull <remote> <branch>

<remote> → usually origin (the default name for your GitHub repo)

<branch> → the branch you want to update (like main or develop)

📘 Common Examples
1. Pull the latest changes for the current branch
git pull


👉 This updates your current branch from its remote tracking branch (e.g., updates main from origin/main).

2. Pull from a specific remote and branch
git pull origin main


👉 Gets the latest changes from the main branch on the origin remote.

3. Pull with rebase (cleaner history)
git pull --rebase


👉 Instead of merging, this reapplies your local commits on top of the updated remote commits — helps avoid merge commits.


| Command             | Behavior                      | History Style      |
| ------------------- | ----------------------------- | ------------------ |
| `git pull`          | Fetch + Merge                 | Adds merge commits |
| `git pull --rebase` | Fetch + Reapply local commits | Linear history     |



4. Pull all branches
git pull --all


👉 Fetches and merges updates for all remote branches.


# after modifying the local repo, instead of adding by " git add " and commiting the repo to local repo by "git commit -m "" , we can do this like below:

git commit -am "This is the 2nd commint from localRepo"


# then push this repo to remote repo:

git push

but it shows error:

DevOps> git push
remote: Invalid username or token. Password authentication is not supported for Git operations.
fatal: Authentication failed for 'https://github.com/manojguha4/Git_traning_2025.git/'


# so for authentication we need to follow the below part:

goto gitHum --> Setting ---> SSH and GPG key --> check the doc and create ssh eky in your local machine and after that add the public key on GitHub.

https://docs.github.com/en/authentication/connecting-to-github-with-ssh

https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent


# create the sshkey on your machine:This creates a new SSH key, using the provided email as a label.

ssh-keygen -t ed25519 -C "manojguha4@gmail.com"




DevOps> ssh-keygen -t ed25519 -C "manojguha4@gmail.com"


<!-- 
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/mguha/.ssh/id_ed25519): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /c/Users/mguha/.ssh/id_ed25519
Your public key has been saved in /c/Users/mguha/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:AJXWFWV/OuPVo7eePtmb80UUEKa5J+1mLtRbQoOQ1Kw manojguha4@gmail.com
The key's randomart image is:
+--[ED25519 256]--+
|    ...o.o*oo+o. |
|     .o .o ++.  .|
|     ..   oo. . o|
|       . E .oo +.|
|        S  ooo=.+|
|           .++.*.|
|          .  ==.+|
|           .+..+*|
|            ..oB*|
+----[SHA256]-----+

Your public key has been saved in /c/Users/mguha/.ssh/id_ed25519.pub
-->

# now cat the .pub key:

cat /c/Users/mguha/.ssh/id_ed25519.pub

ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILDybPhtrzxLrf2rjBXKHiVT+d2T70gK53Vi6vvhK08K manojguha4@gmail.com


# add this key to GitHub:
goto gitHum --> Setting ---> SSH and GPG key --> Add new SSH Key --> add this


# now try with git push:
git push


for the first time it will authenticate via browser or by asking the mail.id. after that it will seemless.

Now we can verify from the remote repo that the commited txt will be visible.



# git branching:

A branch in Git is simply a pointer (or label) to a specific commit in your project’s history.

It allows you to:

Work on different features independently

Experiment safely without affecting your main code

Merge or discard changes when ready.


# 🧭 The Default Branch: main (or master):

When you create a new Git repository:

---->   git init

Git automatically creates your first branch — typically called main (used to be master).

Every new commit you make moves the main pointer forward.

A -- B -- C   ← main



# 🌿 Creating a New Branch:

When you want to work on something new (e.g., a new feature or bug fix), create a branch:

git branch feature-login

This creates a new branch pointer called feature-login that points to the same commit as main.


A -- B -- C
      ↑
    main, feature-login


# To switch to it:

git switch feature-login


Now, any new commits you make move only the feature-login branch.

A -- B -- C -- D -- E
      ↑
     main
               ↑
        feature-login


# 🔁 Merging Branches:

When your feature is done and tested, merge it back into the main branch:

git switch main


git merge feature-login


If no conflicts occur, Git combines the work.After merging:

A -- B -- C -- D -- E
                     ↑
                    main, feature-login


# 🌱 Deleting a Branch:

Once merged, you can safely delete the branch:

git checkout <some other branch>

then,

git branch -d feature-login

If it hasn’t been merged yet and you still want to delete it:

git branch -D feature-login


# 🧩 Checking and Managing Branches:

git branch


# Show all branches including remote ones:

git branch -a


# Rename a branch:

git branch -m old-name new-name

# Check which branch you’re on:

git status


(It’ll show “On branch …”)


# in my setup:

DevOps> ls -l
<!-- total 2
-rw-r--r-- 1 NSN-INTRA+mguha 4096 102 Oct 23 14:46 MyFirstFile.txt
-rw-r--r-- 1 NSN-INTRA+mguha 4096  54 Oct 23 14:04 README.md -->

DevOps> git status

<!-- On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean -->


That means it is the main branch.


# to check the current branch list:

DevOps> git branch 

* main

* -----> as now I am in main branch only.


# crating a new branch:

DevOps> git branch Developer

DevOps> git branch 

  Developer
* main

---> a new branch --> Developr is crated.

# now adding some files in new branch and main branch:

to create a file in Developer branch we need to switch to this branch:

DevOps> git switch Developer 

Switched to branch 'Developer'

DevOps> ls 
MyFirstFile.txt  README.md

----> we can see the both files are present in Developer branch from the main branch. 

Now creating file in Developer branch:

DevOps> echo "this is the samplea file1" >> SampleFile1.txt
DevOps> echo "this is the sample file2" >> SampleFile2.txt
DevOps> 
DevOps> ls 
MyFirstFile.txt  README.md  SampleFile1.txt  SampleFile2.txt
DevOps> 

So there are 2 more file created.

----> now try to commit these files:

git status
git add .
git commit -m "My 1st commit to developwer branch"

git push 

--> it is trowning an error:

fatal: The current branch Developer has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin Developer

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.


--> this error comes as there is no branch created as named Developer in GitHub.

For this we need to perform the below command:

git push --set-upstream origin Developer

-----> it will create the Developer branch in GitHub and push the new codes.


---> now switch to main branch and check whether those files are there or not?

DevOps> git switch main

DevOps> git status
On branch main

DevOps> ls
MyFirstFile.txt  README.md


--->
Now how do we get those files in mian branch:

----> Now we can pull the codes and compare, by pull and compare request from one branch to another in GitHub.

go to GitHub ---> the project ---> pull and compare request --- > pull the code and verify the code and after that merge the code to main branch.

---> after that by git pull --> add this code to local machine in main branch.


DevOps> git pull origin main

DevOps> ls
MyFirstFile.txt  README.md  SampleFile1.txt  SampleFile2.txt


Now the new codes are visible.






# We can merge the code from git also and after that we can push it to GitHub also:

# git merge

The git merge command is used to combine changes from one branch into another.
You usually run it when you’ve finished work on a feature branch and want to bring those changes into the main branch.

🧭 Basic Syntax:

git merge <branch-name>

👉 This means: “Take all commits from <branch-name> and integrate them into my current branch.”

So before merging, always make sure you’re on the branch that should receive the changes.



# 📘 Example

Let’s say your repository has two branches:

main — your stable production branch

feature-login — a branch where you’ve built a new login feature

----> 1. Switch to the target branch (main):

git switch main


----> 2. Merge the feature branch into it:

git merge feature-login


After that:

git add <file>
git commit


# 🧠 Summary

| Command                | Purpose                                    |
| ---------------------- | ------------------------------------------ |
| `git merge <branch>`   | Combine another branch into current branch |
| `git merge --no-ff`    | Force merge commit                         |
| `git merge --squash`   | Merge as a single commit                   |
| `git merge --abort`    | Cancel merge after conflict                |
| `git merge --continue` | Finish merge after conflict resolution     |



# 💡 Merge vs Rebase (Quick Comparison):

| Command      | Behavior                                   | Result                                     |
| ------------ | ------------------------------------------ | ------------------------------------------ |
| `git merge`  | Combines branches with a new merge commit  | Keeps full branch history (with merges)    |
| `git rebase` | Reapplies commits on top of another branch | Linear, cleaner history (no merge commits) |




# ### example ###:


# Create main branch
git init
echo "Initial" > file.txt
git add .
git commit -m "Initial commit"

# Create feature branch
git checkout -b feature-login    ---- It will automatically create this branch and whitched to this branch.

All files are from main branch are also be there in this branch.


(feature-login)$ cat file.txt   ------ same as main.
Initial

Doing some chnages in this file:

(feature-login)$echo "Feature login added" >> file.txt


(feature-login)$ cat file.txt
Initial
Feature login added


(feature-login)$git commit -am "Add login feature"   ----adding in staging area and commiting to local repo.

# check the exsiting brach:

(feature-login)$ git branch -a

  Developer
* feature-login
  main
  remotes/origin/Developer
  remotes/origin/HEAD -> origin/main
  remotes/origin/main


# Switch back to main
git checkout main
echo "Minor changes in main" >> file.txt
git commit -am "Update main file"

# Merge feature branch

(feature-login)$ git checkout main

git merge feature-login
# If conflicts, resolve as explained above


# git reset and git revert:

---> to chec the all commit in oneline:

git log --oneline


# git reset ---soft:

lets say we have a code in main branch and we have modified this code and commit this code, so now we need to reset this commit.

DevOps> vi SampleFile1.txt
DevOps> vi SampleFile2.txt
DevOps> ll

-rw-r--r-- 1 NSN-INTRA+mguha 4096  60 Oct 23 20:01 SampleFile1.txt
-rw-r--r-- 1 NSN-INTRA+mguha 4096  63 Oct 23 20:02 SampleFile2.txt


DevOps> git status

DevOps> git add SampleFile1.txt

DevOps> git commit SampleFile1.txt -m "It is used for soft reset"

DevOps> git log --oneline

1ab9cc0 (HEAD -> main) It is used for soft reset
1c42855 (origin/main, origin/HEAD) Merge pull request #1 from manojguha4/Developer
d81f781 (origin/Developer, Developer)  My 1st commit to developwer branch


DevOps> git reset --soft HEAD~1

DevOps> git log --oneline
1c42855 (HEAD -> main, origin/main, origin/HEAD) Merge pull request #1 from manojguha4/Developer

-----> the commit is removed.

DevOps> git status 

---> here we can see the file is still in modified version. means the staging area.

So, by soft reset ----> git reset --soft HEAD~1 ------> only commit is removed, but file still in modified or in staging area.



# git hard reset:

git reset --hard HEAD~1

It will delete the commit as well as it will also delete the modifcations from the code.



# git revert:

1️⃣ Core Concept

git revert does not delete commits. Instead, it:

Looks at the commit you want to undo.

Creates a new commit that applies the inverse of the changes made by that commit.

Appends this new commit to the current branch.

So your history remains linear and intact, which is why git revert is safe for shared branches.


git revert HEAD


# git diff :

Lets say we are changing some of content in the working area. 

---> git diff <prticular_file> ; --- command we can check which code are being added or deleted.

---> git diff ; --- by this we can check the diffrence of the code in working area with the staging area.



Git_traning_2025 (main)$ echo "This is the topic by which we can compare via git diff" >> SampleFile1.txt 

Git_traning_2025 (main)$ echo "This is the topic by which we can compare via git diff, it is fonr file2" >> SampleFile2.

Git_traning_2025 (main)$ git status 

Git_traning_2025 (main)$ git diff SampleFile1.txt

+ This is the topic by which we can compare via git diff

-----as a new line is added.

Git_traning_2025 (main)$ git diff ; --- if all working files are added in git by [ git add .] --- this coomand witll show nothing.


# check the diffrence bet w2 commit: 

git diff <commit -id1>  <commit -id2>



