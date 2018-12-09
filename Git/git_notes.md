# Git

## Git Overview

Git file statuses primarily follow this sequence:   
*Untracked/Unstaged* -->git add--> *Staged* -->git commit--> *Local Repository* -->git push--> *Remote Repository*

## Project Initiatilization

```
git init // Initialize a new git repository in the current working folder.
git add -A // Add all untracked files to staged (ready to be added to the repo.)
git remote add origin git@github.com:scwestcott/[repo].git // Add remote repo called "origin".
git push -u origin master // Push commit to origin the master branch.
```

If this is the first time working with the remote repo on a given computer, you 
will need to add your public SSH key in your settings in the
remote repo. Copy it to your clipboard from the command line.

```
pbcopy < ~/.ssh/id_rsa.pub
```
## Config

```
git config -l // View current config.
git config -—global user.name “Your Name” // Set name.
git config --global user.email email@example.com // Set email address.
git config --global push.default matching
git config —-global alias.co checkout // Create "co" alias for "checkout"
```

Create/edit the .gitignore file in the root directory of the repo to add files and expressions
that shoudl explicitly be ingored by git. For example, files containing passwords, local config info,
and system created files like .DS_Store. To ignore all files with extention .DS_Store, add this to your
.gitignore file:

```
*.DS_Store
```

## Commits

```
git commit -am "[msg]" // Commit all changes to tracked files (-a) with commit message [msg]  (-m)
git push // Push current branch to the default remote repo.
git commit --amend // Amend the last commit--SHOULD ONLY BE DONE IF NOT PUBLISHED
git checkout [SHA] // Go back to an earlier commit to inspect. Return via: git checkout master
```

## Branching

```
git checkout -b [branch] // Creates a new branch (if [branch] doesn't already exist) and checks it out.
git checkout [branch] // Switch to an existing branch.
git branch // View current branches.
git merge [branch] // Merge [branch] with master.
git branch -D [branch] // Delete [branch], even if unmerged.
git branch -d [branch] // Delete [branch], only if merged.
```

## Abandon Changes

```
git checkout -f // Forget all uncommitted changes and revert to last commit.
git checkout -- [filename] // Abandons the changes in that specific file.
git reset --hard // Resets the staging area and destroys any changes since the last commit.
git checkout -- . // Discard all unstaged files.
```

More info: https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting

## Miscellaneous Commands

```
git log // See a record of our commit.
git log --oneline // Prints one line per commit, with just the out just the subject line.
git shortlog // Groups commits by user, just showing the subject lines
git help [command] // Get help on command, like: get help push
git config -l // List all config variables.
git status // Show the stats of a repository.
git add . // Add all untracked files from the current directory.
git diff // Shows the difference between the last commit and unstaged changes in the current project.
git diff [branch] // Shows differences between current branch and [branch]
git pull // Download any commits from the default remote that local doesn't have.
git clone <URL> // Download source code and create new repo in current directory.
```

### Git Stash

When working on code deplyments for AGG, I ran into an issue where a developer had made changes direclty on the live
server, resulting in a conflict when I tried to pull.

```
./rsync.sh // On local computer. Fetch new files.
git commit -m "Checkpoint live files"
git push
ssh root@[server]
git pull
CONFLICT!
```

Instead do:

```
git stash
git pull
git stash apply
```

Stash takes all local modifications and tucks them away somewhere, it's like a checkout but remembers your dirty state. 
The local tree is clean, so the pull proceeds without conflicts. Then `git stash apply` merges the tucked-away changes 
back into the tree. The merge ends up basically doing nothing, because the local changes were applied in the pull. but 
if there was anything that got missed in the rsync for some reason they'd get put right back in place. Stash is simply 
smarter than pull, if there are conflicts it'll mark them as such.

## Style

From: https://chris.beams.io/posts/git-commit/

1. Separate subject from body with a blank line
1. Limit the subject line to 50 characters
1. Capitalize the subject line
1. Do not end the subject line with a period
1. Use the imperative mood in the subject line
1. Wrap the body at 72 characters
1. Use the body to explain what and *why* vs. *how*

Rule of thumb for subject line, complete this sentence: If applied, this commit will _your subject line here_

## Further Reading

1. [Learning Enough Git to be Dangerous](https://www.learnenough.com/git-tutorial)
1. [How to Write a Git Commit Message](http://chris.beams.io/posts/git-commit/)
1. [GitHub Git Tutorial](https://guides.github.com/activities/hello-world/)
1. [BitBucket Tutorial](https://www.atlassian.com/git/tutorials/)
1. [Pro Git (free e-book)](https://git-scm.com/book/en/v2)
