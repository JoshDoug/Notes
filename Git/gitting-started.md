# Getting started with Git - Installation & Configuration
Install by downloading and running .pkg/.exe from git-scm.com
Or, brew install git.

Run `git --version` to make sure it has installed successfully.

VCS - Version Control System
SCM - Source Control Management

## History
SCCS - Source Code Control System
* 1972, closed source, bundled free with Unix

RCS - Revision Control System
* 1982, open source, cross platform, faster, stores most recent file and then snapshots of changes to move back. Faster than SCCS.

CVS - Concurrent Versions System
* 1986-1990, open source, tracks changes in more than 1 file, tracks sets of file, an entire project (unlike SCCS or RCS), also allows a remote repository to be used that can handle more than one user editing a file at a time(?).

Apache Subversion (SVN)
* 2000, open source, snapshot directories not files - a directory has a state not a file. This could handle filename changes better than CVS.

BitKeeper SCM
* 2000, closed source, proprietary, distributed version control (DVC)

Git
* 2005, open source & free, distributed version control, cross platform

## Configure
Git stores configuration information at three levels/in three places.
* System
* User
* Project/Local

E.g.
```
git config --system user.name "Joshua Stringfellow"
git config --global user.name "Joshua Stringfellow"
git config --local user.name "Joshua Stringfellow K1460846"
```

To list configurations: `git config --list`

Other configurations:

`git config --global core.editor "vim"`
`git config --global core.editor "vim -wl1"` Not sure if this is just for mate?
`git config --global color.ui true`

Git Autocompletion:
In the home directory run (that's a capital 'oh' not a 'zero'):
`curl -OL https://github.com/git/git/raw/master/contrib/completion/git-completion.bash`

### System
These configurations will be the default for every user on a computer, but they can be overridden.
Typically in /etc/gitconfig

### User
NIX : `~/.gitconfig`

Windows : `$HOME\.gitconfig`

### Project
my_project/.git/config

## Git Help
Using `git help`

# Using git
Initialise a git repo in the root of a project directory: `git init`

## Git Status
Reports the current status of the current branch in git: `git status`

Reports the difference between the working directory, staging index, and the repository. Also reports the current branch.

## Add files to git:
Used to add new files or edit files to the staging index

* Add all: `git add .`
* Add specific file: `git add HelloWorld.java`
* Add several specific files: `git add file1.txt file2.txt`
* Add with wildcards: `git add file*` could add file1.txt and file2.txt

## Remove files from git
If you simply delete a file from the folder it will still show up in git status, to remove it run 'git rm fileToDelete.txt' and then commit that change, as you would a git add.

Can also use `git rm fileToRemove.txt` to remove from git, delete it, and stage the change ready to be committed in one go, this will erase it though, not put it in the Trash or stop tracking it.

## Moving files in git
### Manually:
If the file is manually renamed, then git thinks a file has been deleted and a new file has been added, if the original file is `git rm file.txt` removed and the renamed file is added, then running git status will show that git has at this point realised the file was just renamed (even if they aren't identical, just similar), it can then be committed normally.

### With git:
As is typicaly on NIX, moving and renaming can both be done with mv, it works the same with git: `git mv ogfile.txt aDirectory/newfilename.txt`, this will move it into a the directory, rename it, and add it to the staging index as well.

## Git Commit
Commit messages can have a short single-line summary with an optional lengthier description. Commit messages should describe the changes and the effects in the present tense, what the commit does not what you have done. E.g. "fix bug", "fixes bug", not "fixed bug". Although the commit itself should be more descriptive..which bug? Fix bug is too vague, be clear and descriptive. Also keep it relevant to the commit, don't include comments that aren't about the commit e.g. "we should discuss this later" - bad, save that for email/JIRA/etc.

Commit: `git commit -m "Commit Message"`
* -m for message

Add & Commit: `git commit -am "Commit Message"`
* use carefully

### Amending Commits
You can't amend any commit later than the current most recent commit that HEAD is pointing to.

`git commit --amend -m "Changing commit message to something useful"`
Can be used to change code committed, or even just the commit message.

### Retrieving old Versions
Instead of amending older commits (which would violate git's data integrity) you can make new commits which undo what was done in the older commits - ensures the log of commits is accurate.

Resetting a file to a specific point:
`git checkout 290salkd94wq -- file.txt` where 290sa.. is the hash for the commit you want the file to be reverted to. This file is then put in the staging area.

Reverting using the git revert command:
`git revert 290salkd94wq`
This will open up your editor to give you a chance to edit the commit message. The command simply flips all the changes from the previous commit (deletes additions, adds deletions) and immediately commits it.

## Undo Changes
### Undo changes in the working directory
Undo changes on a file: `git checkout -- file.txt`
The `--` is used to avoid a potential name conflict with a branch, as git checkout can also be used to switch to another branch.

### Unstaging files from staging index
Useful if you've grouping commits into sensible steps (if you've fixed two different bugs in one session they should probably still have separate commits) and you've accidentally added/staged files you don't want to commit.

`git reset HEAD file.txt`

### Git Reset
Powerful yet dangerous, moves the HEAD pointer to an earlier commit so that you can start from there.

There are different types of git resets: Soft, Mixed, Hard

#### Soft Reset - the safest reset
Soft moves the HEAD pointer to the specified commit, but it doesn't change the staging index or the working directory at the same time. It just moves the pointer. So the repository is at an earlier version, but the working and staging directories are the same as they were before the reset. So if you committed everything you would be back to where you were before the reset, but your git log/history would be messed up. You could run a diff to see all the changes that have happened from the commit where the HEAD has been reset to.

`git reset --soft <commit hash>`

If you reset to an earlier commit, you can still move back to the latest by running reset again, with the commit hash of the latest commit. But you will need to have this saved somewhere because git log will not show it anymore (it will only show commits up to the current point where the HEAD is). What happens if you've made changes and commits since and want to revert back? I do not know, TODO: find out. -- Seems like new commits will obliterate any commits beyond where HEAD is pointing.

#### Mixed Reset
Moves the repository back to the commit, changes the staging directory to match the repository, but leaves the working directory alone.

`git reset --mixed`

#### Hard Reset
Moves the repository, staging index, and working directory back to the point of the commit (staging and working will be the same as the repo) and everything that was committed after that commit will have been obliterated. Use only when absolutely necessary.

You could still revert to the latest commit, but any working or staging index changes will have been lost. And this wont be an option after making further commits. (I think -hmm maybe not. It would eventually get 'garbage collected' but if you saved the hash it would be accessible, apparently).

`git reset --hard`

## Git diff
Compare working directory and repository: `git diff`
Or working and staging if there are differences there?

Diff for a specific file: `git diff file1.txt`
Diff for a staged file: `git diff --staged file1.txt`
Diffs the staged file vs the repo, not the working dir

Diff just the changed words: `git diff --color-words file.txt`

Diff branches: `git diff origin/master..master`
Best to put the branch that is behind first (otherwise newer additions will show as deletions and vice versa)

So if you have a file that has been committed, then that same file has been edited and staged and then that same file has been edited again so that it has different version in the working dir, staging index, and repository, then *git diff* will show difference between working and staged and *git diff --staged* will show difference between staged and repository.

## Git logs
Get the commit log: `git log`

Display last 5 commits: `git log -n 5`

Get commits from a date: `git log --since=2017-03-20`

Get commits until a date: `git log --until=2017-03-21`

Can combine since & until for a date range.

Get commits from a specific author: `git log --author="Joshua"`
The author name doesn't have to match exactly.

Grep commits: `git log --grep="Init*"`
This will only grep messages, not authors etc.

Squash log: `git log --oneline`

## Git Clean
Remove untracked files

Test run (shows what would be removed but doesn't do anything):
`git clean -n`

Removes any untracked files (deletes them):
`git clean -f`

# Git Head
Just a pointer that points to the most recent commit on the current branch.

Interact with head:
* `cat .git/HEAD`
* `git log HEAD`
