- Version Control System(Centralized/Distributed).
## Setup
### levels
- ***system*** : all users
- ***global*** : all repos of user
- ***local*** : current repo
### config
 ```
git config --global user.name "3arfi"
git config --global user.email bz9a@gmail.com
git config --global core.editor "code --wait"
git config --global core.autocrlf input
```
## Initializing repo
```
mkdir repo_name
cd reponame
git init
```
## Git workflow
```
echo hello > new_file
git add new file 
git commit -m -a (all : youn can use it without add) "first commit..."
```
## Removing files
```
rm file
git ls-files
git rm *.txt
```
## Rename files
```
git mv file new_file
```
## Ignoring files
```
echo /log > .gitignore
git add .gitignore
git commit -m "added gitignore"
```
## Short status 
```
git status -s
```
## View staged and unstaged changes
```
git diff --staged (commit vs staged)
git diff (staged vs unstaged)
```
## Visual diff tools
```
git config --global diff.tool vscode
git config --global diff.tool.cmd "code --wait --diff $LOCAL $REMOTE"
```
## Viewing history
```
git log
git log --oneline
```
## View commit
```
git show 7356c02
git show HEAD (last commit)
git show HEAD~3 (starting from head)
git show HEAD~3:file (final version)
```
## Unstaging files
```
git restore --staged file *.txt
```
## Discarding local changes
```
git restore main.js
git clean -fd (undo local changes)
```
## Restore a file to earlier version
```
git restore --source=HEAD~1 file.txt
```