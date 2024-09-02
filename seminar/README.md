# git

Version control :-
version control is software that tracks and manage changes to files over time.

1] revisit earlier versions of the files, compare changes between versions, undo changes, and a whole lot more.
2] Git, Subversion, CSV, and mercurial, etc.

Git useCase :-
1] Track changes across multiple files.
2] Compare versions of a project.
3] Time travel back to old versions.
4] Revert to a previous version.
5] Collaborate and share changes.
6] Combine changes.

Meta info :-
1] Linus Torvalds 2005 wile working Linux using BitKeeper for version control (BitKeeper change for money) created Git
2] Git run locally on the machine (no account and internet required)
3] Github is a service that hosts repositories in the cloud and makes it easier to collaborate with other people (account and internet is required).

Git Bash :-
1] Git designed to run on Unix-based interface (Bash). It is the default shell for Linux and Mac.
2] Window has Command Prompt no unix-based.

## Git Verison

`git --version`. //git version 2.43.0

`git config user.email "c-shubham.shinde@amagi.com"`
`git config user.name git-shubham-shinde`

`git config --global user.email "c-shubham.shinde@amagi.com"`
`git config --global user.name "shubham s"` //in quotes other wise it will skip the things after space

Repository :-
A Git "Repo" is a workspace which tracks and manages file within a folder. (each repo has it own histories and contents)
Below command will log og commit of given repository
`git log` //we can see commit hash(a long id) in log
`git log --abbrev-commit` //for short commit hash
`git log --oneline` // sort for --pretty=oneline --abbrev-commit //give short commit hash and first line of commit message of each

To initialize any folder as new git repository it create a .git folder which store the commit histories.
`git init`

Current status of current git repository and its content
`git status`

**staging area** the changes.

- most of the time untracked file are computer generated file which we don't want to commit.
- If you created new file it will be untracked they don't belong to version control
  remember :- if file A is tracked but you decide to untrack now when you go back to old commit/version git will not replace the untrack file with old tracked same file A.
- Also if we have tracked file then we decide to add it to .gitignore git will still track it so we have to untrack it first
  `git rm --cached filename`
- To unStage a file
  `git restore --stage filename`

**working directory -> `git add` -> staging area -> `git commit` -> repository**
`git add .` //add all the files
`git add filename`
`git add filename1 filename2`

**commit**

- each commit will have reference to parent hash code (SHA 1 algorithm)
- **Atomic commit** single feature,change, or fix.(keeping each commit focused on a single thing)
- for git message use present-tense imperative style
- commit is kinda checkpoint in git repository.
- git commit will commit changes to the repository from staging area
  `git commit` //will open vim or text editor to input message //To configure to use vs code instead of vim for longer message //https://git-scm.com/book/en/v2/Appendix-C%3A-Git-Commands-Setup-and-Config
  `git commit -m "my message"`
  `git commit -a -m "message"` //stage all and commit with message //not add untracked file
  `git commit -m "message" -m "description"`

**Amending Commits**

- to roll back and commit again
- before doing so first modify file that you want and add file to staging area\
- `git commit --amend` //opens text editor for commit message of previous commit

**branches**

- branches allow us to create alternate timeline, separate context
- many people treat master branch is "source of truth" or "official branch"
- Github use main and git use master as default branch name
- branch is reference to some commit
  `git branch` //show all branch and active branch has \* as prefix
  `git branch -v` //show all branches with additional details (active branch, head, latest commit)
  `git branch branchName` //create new branch from current reference/Head but doesn't switch head to that new branch.
  `git switch -c branchName` //-c = create new branch and switch to it
- (HEAD -> main, origin/main, origin/HEAD, test-branch) head is point to "main", "test-branch" even when we don't point to
- if we switch to new branch and commit something
- commit cc890223f4ad01b091562cd482e46e2224706250 (HEAD -> test-branch) //head pointing to test-branch
- commit 3e5592d230da63bb2466291cc6bd624b7d65a969 (origin/main, origin/HEAD, main) //main is still point to latest commit on it branch
  `git log`
- if we have unstage changes before switching we have to commit or stash then we will be able to switch
- untrack file will let you switch and that file will still present in the branch you switch to
  `git switch branchName` //it is new command //head will point to test-branch now
  `git checkout branchName` //switch to the branchName
- `git checkout -b branchName` //create new branch and switch and make head point to it

**deleting branch**

- `git branch -d branchName` //we can't delete if we are on that branch //the branch has some commit message we have to merge it first
- `git branch -D branchName` //we can't delete if we are on that branch

**renaming branch**

- `git branch -m newBranchName` // -m --move move/rename //we have to be on that branch to rename it
- `git branch -m oldBranchName newBranchName` //we don't have to be on that branch

**head**

- HEAD is a pointer/reference that refers to the current "locations" (branch pointer) in repository.
- It points to a particular branch reference.
- `cat .git\HEAD` //ref: refs/heads/main //navigate to this folder in .git then main file will contain the hash code for it latest commit as mention in`git log` to which head point.

**ignoring file**

- Secrets, API keys, credentials, etc. OS files (.DS_Store on Mac), Log files, Dependencies & packages.
- `node_modules/` the forward slash tell it is directory and not file

**merging**

- allow use to incorporate changes from one branch into another.
- we merge to the current HEAD branch
  `git merge branchName` // merge branchName into current branch that we are on
- fast forward merge :- case of merge where we diverge to new branch and made some commit to that new branch then when we merge it to master(no further commit after divergence) then master will catch up to that new branch.
- if there are conflict git will create a merge commit(this commit has two parent) after we resolve the conflict.
- if you resolve it manually and git didn't create merge commit then you can add file and commit manually saying resolving conflict.

**Diff**

- safe and informative command
- without other options it lists all the changes between working directory and staging area. but when we add all file staging area then there is not difference left.
- git diff command to view changes between commits, branches, files, our working directory, amd more.
- we also combine it with git status and git log to better picture of a repository and how it changed over time.
- `git diff` //show changes from unstaged and tracked file from working directory and compare with staging file.

```
diff --git a/char.txt b/char.txt       //for each comparison git explain which two file it is comparing.(two version of same file A, B)
index 2444340..3747bcf 100644          //metadata :- hash code of two file being compare
--- a/char.txt                         //"-" sign for file "a"
+++ b/char.txt                         //"+" sign for file "b"
@@ -1,7 +1,8 @@                        //chuck head
-One
-Two
+
+
 Three
 Four
+two
 Five
 Six
 Seven
@@ -14,7 +15,8 @@ Thirteen               //chuck head
 Fourteen
 Fifteen
 Sixteen
-Seventeen
-Eighteen
 Nineteen
+four
+five
+six
 Twenty
```

- comparing file in different point in time (we can set it if we want)
- big file only small chuck is show which is affected
- line start with - represent change coming from file 'A' (staging area)
- line start with + represent change coming from file 'B' (working directory)
- @@ -14,7 +15,8 @@
- -14,7 = 7 line are coming from file A(-) starting from line number 14 (line that are affected / or shown)
- +15,8 = 8 line are coming from file B(+) starting from line number 15 (line that are affected / or shown)

2]
`git diff HEAD`

- lists all changes in the working tree since your last commit (or head).
- (compare last commit with working directory) OR
- (compare last commit with staged and unstaged changes)
- ---/dev/null ('-' sign file is null)= good for untracked file as when we add it stage `git diff` will show nothing but `git diff head` will show it.

3]
`git diff --staged` OR `git diff --cached`

- list the changes between the staging area and our last commit.
- (compare last commit with staged changes)

4]
`git diff HEAD filename.extension`

`git diff HEAD folder/filename.extension`

`git diff HEAD folder/filename.extension file2name.txt` //two file changes

- narrow down to see changes from the specific file

5]
`git diff branch1..branch2` //order matter
`git diff branch1 branch2`

- will list the changes between the tips of branch1 and branch2

6]
`git diff commitHash1..commitHash2`
//OR
`git diff commitHash1 commitHash2`

- you can copy the commit hash from `git log --oneline`

**stash**

- avoid unnecessary commit or pollute commit history.
- stash changes and come back later. running `git stash` will take unstaged and staged file (not untracked files) and stash them
- while switching :-
- untracked file change will come along with you (also tracked file but no conflict will let you switch)
- tracked file conflict change are there git will not allow us to switch
- we can stash and pop mutiple times just like stack FILO.
- `git stash` sorter version of OR `git stash save`
- when apply or pop we can get merge conflict
- `git stash pop` recently stashed changes and apply to working directory and remove it from stash list
- `git stash apply` recently stashed changes and apply to working directory and don't remvoe it from the stash list
- `git stash list` to see list of stashed changes
- `git stash apply stash@{1}` apply specify stash using stash ID
- `git stash drop stash@{2}` to remove the stash using stash ID
- `git stash clear` to empty entire stash

**Undoing changes and Time Traveling**

- Usually, head points to a specific branch reference rather than a particular commit.
- when checkout to particular commit, HEAD points at that commit rather than at the branch pointer.
- "detached head state" thing we can do 1] copy old version of file, 2] create new branch from that point, 3] come back to branch  
  `git checkout <commitHash>` //"detached head state" //change should be committed before switching
  `git checkout branchName` OR `git switch branchName` //to switch back to the branch

- referring to previous commit relative to particular commit.
- HEAD~1 refers to the commit before HEAD (parent).
- HEAD~2 refers to 2 commits before HEAD (grandparent).
- `git checkout HEAD~3` //will not ditach head i think //one point before head //we can use mutiple time (i.e :- n=3) to go one commit back at time from current head position

- `git switch -` //if you detach head like this just once `git checkout <commitHash>` then we can use this command to go back to the previous branch

- `git checkout HEAD fileName.txt` //discard changes of fileName.txt from working directory and staged area and restore by last committed file version
- `git checkout HEAD fileName.txt fileName2.ts` //we can specify multiple files
- `git checkout -- fileName.txt` //same as `git checkout HEAD fileName.txt` restore to head position
- Working Directory :-

- `git restore fileName.txt` //if file is from working directory(not staged) discard changes and restore by last committed file version
- Staging area
- `git restore --staged fileName.txt` //file will be just unstaged

- `git restore --source HEAD~5 fileName.txt` //IMPORTANT //to change default source HEAD we can use --source option //restore file to old version of it //note working directory change will lost if not committed //`git restore fileName.txt` to change file version to latest one which is HEAD
- `git restore --source HEAD~5 fileName1.txt fileName2.txt`

- Git Reset :- To undo the commits.
- reset the repo back to a specific commit.
- moves the branch pointer backwards, eliminating commits.
- `git reset <commitHash>` // remove all the commits did after the given commit hash i the remove commits change will be shown in working directory as unstaged
- `git reset --hard <commitHash>` // remove all the commits did after the given commit hash i the remove commits change will be also removed
- `git reset --hard HEAD~1`

- Git revert :-
- it create brand new commit which reverse/undos the changes from a commit. Because it result in a new commit, you will be prompted to enter a message
- reverse commit that other people already have on there machines, without altering commit history.
- `git revert <commitHash>` //doesn't remove the given commit and preciding commit //instead it will get all the commit happen after and current given hash code and show it in working directory //and also create a revert commit for us which we can procced after fixing code and resolving merge conflict.

- revertB branch was created from commit 6 so even when we deleted old commit starting from commit 3 that branch was not affected

```
4f626b2 (HEAD -> main) reset upto 3
cdc7eab commit 3
a01f936 commit 2
60d9622 commit 1
3af487b updated
```

```
d623523 (HEAD -> revertB) Revert "commit 3"
5d897d2 updated 10 37 56 67 89
509c50e updated 1 3 56 4 67
5976aad commit 6
1c28e19 commit 5
e4c75a4 commit 4
cdc7eab commit 3
a01f936 commit 2
60d9622 commit 1
```

GitHub :-

- Github is a hosting platform for git repositories. You can put your own Git repos on Github and access them from anywhere and share them with people around the world.
- Beyond hosting repos, Github also provides additional collaboration features that are not native to Git (but are super useful). Basically, Github helps people share and collaborate on repos.
- the world's largest host of source code.
- home to the code in cloud
- code backup, collaboration
- open source projects

**cloning**

- get local copy of an existing repository
- `git clone <URL>` //setup up file and folder //set commit history //setup remote

- Exiting local repo on machine
  1] Create a new repo Github.
  2] Connect your local repo (add a remote).
  3] Push up your changes to Github.
  -steps :-
- create empty repsoitory on github

- set up destination remote repository of the github to push up to.
- `git remote -v` //
- `git remote add <name> <url>` //remember the (url) using the (name) (most of the time name is always 'origin' it is standard name for remote) whenever we say 'origin' it refer to URL
- `git remote add origin https://github.com/Shubham-code-lab/del-later.git` //origin is kinda key to url. //open source project can have multiple remotes
- `git remote rename <oldName> <newName>`
- `git remote remove <name>`

- to not push all branch to github we specify just one branch
- `git push <remote> <branch>` // git push origin main
- `git push origin master` //this will push local branch to remote branch if branch doesn't exist it create new branch master on remote github if it doesn't exist //so, rename local branch if it was master to main if want our branch name as main
- `git push origin master:main` //push local master branch changes to remote main branch.
- upstream option :-
- -u allow use to set upstream of the branch (link local branch with remote branch)
- `git push -u origin main` //local machine main branch is connected to remote main branch so next time we can just so `git push`
- `git push -u origin master:main` //local machine master branch is connected to remote main branch so next time we can just so `git push`

- new repository fom Github
  1] Create a brand new repo on Github
  2] Clone it down to your machine
  3] Do some work locally
  4] Push up your changes to Github

**Fetching & Pull**

- when we clone repository we have two branch reference pointing to same commit "master" and "origin/master"
- "master" regular branch reference
- "origin/master" remote tracking branch reference to the state of master on the remote.(last commit on master branch on origin). most recently know state of the master branch on the remote
- `git branch -r` //gives list of remote tracking branch //
- `git checkout origin/main` //detached head we can create new branch from here if we want
- `git push origin main`

- `git clone <URL>` //git will connect local machine default branch with remote default branch (same name of remote)
- `git checkout remoteBranchName` OR `git switch remoteBranchName ` //git will connect local machine default branch with remote default branch (same name of remote)

- `git fetch origin` //default is "origin" so no need to write it //download code from remote repository and update the local repository //but not integrated in working directory
- `git fetch origin branchName` //we can also only fetch one branch //only remote tracking origin/branchName will update
- `git checkout origin/branchName` //we can see the changes here but not on "branchName" can also `git log`
- `git pull origin branchName` // `fetch`update remote tracking branch and `merge`update current branch with remote tracking branch
- `git pull` //as git switch config the tracking // git assume remote is origin and branch will be the tracking config of current branch
