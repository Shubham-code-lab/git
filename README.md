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
  `git commit -a -m "message"`   //stage all and commit with message
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
`git branch`   //show all branch and active branch has * as prefix
`git branch branchName`  //create new branch from current reference/Head but doesn't switch head to it.
- (HEAD -> main, origin/main, origin/HEAD, test-branch)      head is point to "main", "test-branch" even when we don't point to 
- if we switch to new branch and commit something 
- commit cc890223f4ad01b091562cd482e46e2224706250 (HEAD -> test-branch)       //head pointing to test-branch
- commit 3e5592d230da63bb2466291cc6bd624b7d65a969 (origin/main, origin/HEAD, main)    //main is still point to latest commit on it branch
`git log`  
`git switch branchName`  //head will point to test-branch now 

**head**
- HEAD is a pointer/reference that refers to the current "locations" (branch pointer) in repository.

**ignoring file**

- Secrets, API keys, credentials, etc. OS files (.DS_Store on Mac), Log files, Dependencies & packages.
- `node_modules/` the forward slash tell it is directory and not file


