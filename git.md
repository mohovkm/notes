### Patch
Create patch file from diff and patch another file

```bash
diff -u UpdatedFile > PatchFile

patch OriginalFile < PatchFile
```

### Undo patch
```bash
patch -R OriginalFile < PatchFile
```

### Stash

```bash
git stash
git stash list
git stash aply 1 # index from stash list
git stash pop # retrieve stashed data
git stash --include-untracked
git stash push -p # push changes to shash and ack for every change/file
```

### Clean
Cleaning git local repo for untracked files and folders
```bash
git clean -n # dry run
git clean -d # delete directories
git clean -f # delete all (force)
```

### Reset HEAD
```bash
git reset HEAD --hard
```

### Reset single file
```bash
git checkout HEAD -- my-file.txt
```

### Move 1 commit from master to feature permanently
#### You are on the branch master right now
```bash
git log # to see all commit hashes
git checkout {hash of previouse commit} # Switching to the previouse commit
git checkout -b feature/new-branch # Creating new branch
git cherry-pick {hash of last commit that we need to move} # Moving commit to the new branch
git checkout master  # Swithcing to the master branch
git reset --hard HEAD^  # Resetin gmaster branch to drop errors
```

### Rebase your feature onto new changes in master
```bash
git checkout mainline
git pull
git checkout feature/your-branch
git rebase mainline
```

### Merge multiple commits into 1 with rebase
#### Number 5 is presening number of commits that we want to merge, starting from current HEAD
- run following code:
```bash
git rebase -i HEAD~5
```
- replace `pick` with `squash`, starting from the second line
- save the file
- change or leave commit messages, save the file
- push your changes to the remote with following code:
```bash
git push --force-with-lease origin HEAD
```

### Restore
#### Restore single file from commit
```bash
git checkout [commit hash] -- path/to/file
```

#### Restore deleted files
```bash
git ls-files -d -z | xargs -0 git checkout --
```

### Rename branch (local and remote)
```bash
git checkout old-name
git branch -m old-name new-name
git push origin --delete old-name
git push origin -u new-name
```

### Merging without conflicts with accpetion ours (current branch) or theirs (branch that we merge into current)
```bash
git checout master
git merge feature/mybranch --strategy-option theirs
```


### When you have merge conflicts and want to change history of you branch, to resolve and avoid them
1. Make sure, that your git is clean, working tree is empty, etc
2. Checkout your branch your'e wanting to change (squash). Let's name it "feature/mybranch"
3. Find the last common ancestor (commit hash, let's say it b1234) for your branch and the conflict branch (between "feature/mybranch" and "master")
4. Squash commits, add files to stage, commit them

```bash
git reset b1234
git add .
git commit -m "Changes for all files in 1 commit"
```
5. Rebase onto conflict branch
```bash
git rebase origin/master
```
6. When rebasing you could face conflicts. Resolve them manually or automatically with `checkout`. 
NOTE: under `--theirs` will be your current file (not `--ours`, don't know why, after doing this don't forget to check)
```bash
git checkout --theirs your_file_with_conflict.py
```
7. Add changed files and continue rebasing. 
```bash
git add .
git rebase --continue
```
8. Push local changes to remote. (don't forget to check files and commits before pushing)
```bash
git push --force
```


### Rename origin
```bash
git remote --verbose # to see existing remotes
origin  git@github.com:mohovkm/old_name.git (fetch)
origin  git@github.com:mohovkm/old_name.git (push)
git remote set-url origin git@github.com:mohovkm/new_name.git
git remote --verbose
origin  git@github.com:mohovkm/new_name.git (fetch)
origin  git@github.com:mohovkm/new_name.git (push)
```


### Add to stage all files except one:
```bash
git add . ':!path/to_your-file/dot.txt'
```


### Beautiful logs:
~/.gitconfig:
```
[alias]
lg1 = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
lg2 = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' --all
lg = !"git lg1"
```


### Change last commit message
```shell
git commit --amend -m "new message"
```

#### Add new files and change commit
```shell
git add some-new-file.py
git commit --amend -m "new message"
```

#### Show only commit messsage (to change it later for exmaple)
```
git log -1 --format=%B | xargs
```

#### Copy to clipboard and change commit message:
```
git log -1 --format=%B | xargs | pbcopy
git commit --amend -m "$(pbpaste)"
```


### When you forgot to track remote, and need to set it manually
```bash
git branch -u origin/mainline
branch 'mainline' set up to track 'origin/mainline'.
```

### Unstage committed file
`git rm --cached <filePath>` does not unstage a file, it actually stages the removal of the file(s) from the repo (assuming it was already committed before) but leaves the file in your working tree (leaving you with an untracked file).

`git reset -- <filePath>` will unstage any staged changes for the given file(s).
