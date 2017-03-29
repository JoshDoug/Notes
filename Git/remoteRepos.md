# Using local and remote repositories, and branches
Locally git is just the master and any branches you've added.

When you begin to use a remote, there's a couple of things to note. When the remote is pushed to for the first time (ie to create the remote repo) it creates a master branch with an identical set of commits to the branch (let's say master for this explanation) that you pushed. But your local repo also creates an origin/master branch (doesn't have to be origin) that is also the same as the remote and local master. This origin/master branch can then be used as the branch that tracks changes on the remote when you fetch from the remote, where git can store and merge the changes without affecting your local master.

## Git Clone
`git clone https://url-for-git-project.com/user/project.git`
This will clone into a new directory with the name of the project used on the remote branch

`git clone <url> <localName>`
This can be used to specify the name of the project folder locally, if you want it to be different for whatever reason.

## Managing a remote:
Add remote: `git remote add origin https://url-to-git-repo.com/path.git`

`git remote add <alias> <url>`

List remotes: `git remote`

List more info about remotes: `git remote -v`

Remove remote: `git remote rm origin`

## Push - push changes to remote
`git push -u origin master`
Using -u also sets up the remote tracking branch (TODO: Read up on this and explain better)

Once the tracking branch is set up (seems to be automatically set up to origin/master when cloning which is nice) just need to use `git push` to push to the tracking branch. (TODO: Read up on tracking branch)

Pushing to a remote will push whatever the current branch is.

e.g. `git push origin different_branch` push to origin..not origin master. Origin just refers to the remote repo as a whole, specifically in git it refers to the url of the remote repo, `cat .git/config`

To set up tracking on a new branch, you can do so when you push `git push -u origin new_branch` (need to double check that), or `git branch --set-upstream new_branch origin/new_branch` - this should definitely work. -u is the shorthand for --set-upstream.

You cannot push to a remote when your branch is behind, you have to pull/fetch & merge those changes and then push. It doesn't matter if there aren't any conflicts, you have to be on the latest commit. Right? Seems so.

## Fetch - download changes from remote (but don't merge them)
`git fetch`

Fetch will find any new commits and new branches. The branches themselves aren't downloaded, but git now has a reference to them which you can use to pull them down as well.

Always fetch before you work.
Fetch before you push.
Fetch often.

## Merge - merge changes from fetch (or another branch)
In this context we're looking at fetching from a remote

Fetch before you work
Fetch before you push
Fetch often - no reason not to do it often

You want to switch to the branch (typically master) that will receive the merged changes. So if you're on a feature branch and you want to merge that feature back into master, then switch to master, `git checkout master` and merge: `git merge feature_branch`

`git diff origin/master..master`

`git merge origin/master` merges with the local origin/master.
merge will merge the origin/<branch> with the associated tracking branch

### Fast Forward Merge vs True Merge
A fast-forward merge is when the branch being merged is ahead of the branch (typically master) that is receiving the changes.

To stop git from doing a fast-forward merge use: `git merge --no-ff <branch>` It might be worth doing this if you want to specifically document that you've done this merge, you don't want it to be easy to miss in the log.

To only merge if a fast-forward is possible: `git merge --ff-only <branch>`

A true merge is when a branch is merged into another, but the branch that is receiving the changes is ahead of the other branch/has different additional commits. This is referred to by git as a "merge made by the 'recursive' strategy".

### Merge Conflicts
When the same line is changed in two different branches and the branches are merged. In these cases git will paused the merge in the middle showing the branch as e.g. `master|MERGING`, tell you there's a conflict and mark the conflict in the file.

When there's a conflict there are 3 choices to resolve the conflict:
* abort the merge (and figure it out later)
* resolve the conflicts manually
* use a merge tool

#### Aborint the merge:
While in the `master|MERGING` state just run: `git merge --abort` and you'll be back to where you started before attempting the merge

#### Manually resolving:
Inside the files with the merge conflicts git marks them like so:

For example:
```
<<<<<<< HEAD
this is an example
=======
this is a slightly different example
>>>>>>> a_branch
```

To resolve, just manually merge the changes together as you like, and delete the duplicate part along with the markers placed in by git. Then add and commit the changes, you don't necessarily need to add a message as git will provide a default merge commit message.

#### Merge Tools:
Run `git mergetool` and git will provide a list of recommended(?) merge tools.

Run `git mergetool --tool=toolName` to use the tool (probably need to install the tool first)

#### Avoiding Merge Conflicts
Simple strategies that can help avoid merge conflicts
* keep lines short (if a line has to be broken into several to show on the screen, it's harder to see where the conflicts actually are)
* keep commits small and focused
* beware stray edits to whitespace - spaces, tabs, line returns
* merge often
* track changes to master (pull from master)

## Pull - fetch and merge changes

`git pull` is really `git fetch && git merge`

## Branches
Does this make sense in this file? Not really.

* `git branch` view branches (but not remotes)
* `git branch newbranch` create a new branch called newbranch
* `git branch -r` lists remote branches
* `git branch -a` lists all branches

Switch branches: `git checkout test_branch`
Create branch and switch to it: `git checkout -b new_branch`

Comparing branches:
`git diff branch1..branch2`

Renaming branches: `git branch -m new_feature better_name` rename new_feature branch as better_name, -m is the same as --move

Deleting branches, switch to master first (cannot delete the branch you are currently on): `git branch -d branch_to_delete` -d or --delete

If you have unmerged commits then git will warn you not to delete it, but you can override this by passing -D instead of -d.

Show current branch on command prompt:
Add the file to prompt and source it (like .git-completion.bash etc)
https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh

On macOS or Linux add following to bashrc: `PS1='$(__git_ps1 "(%s)")\u:\W\$ '` where `$(__git_ps1 "(%s)")` is the important part for showing the branch. The rest is just additional prompt example additions.

On Windows: should already be setup when installing git! If not you can create and edit a bash_profile or bashrc used within git bash. E.g. `export PS1='\W$(__git_ps1 "(%s)") > '` saved as .bash_profile in the normal windows user home directory.

### Remote Branches
Checking out remote branches:
`git branch <branch> <origin>/<branch>` and switch to it `git checkout <branch>` or in one go: `git checkout -b <branch> <origin>/<branch>`

Deleting a remote branch, there are two ways:

Old - `git push origin :<branch>`, this will only remove the remote branch, you will still have the local branch if you pulled it.

New - `git push origin --delete <branch>`

# Collaborating
Using github: fork the repo, which will fork it to your github profile. Then you can make the changes, commit them and push them up to your forked repo, at which point you can issue a pull request on the main project repo.

## Collaboration workflow
Write up later, in short:

Person 1
1. `git checkout master`
2. `git fetch`, `git merge origin/master` or `git pull`
3. Create branch `git branch <branch>`, and switch to it `git checkout <branch>`, or `git checkout -b <branch>`
4. Make and add changes: `git add changes.txt`
5. `git commit -m "Some changes"`
6. `git fetch` (just in case)
7. `git push -u origin <branch>`

Person 2, e.g. a coworker's collab workflow:

1. `git checkout master`
2. `git fetch`, `git merge origin/master` or `git pull`
3. `git checkout -b <branch> origin/<branch>`
4. `git log`, `git show <hash>`
4. Make and add changes: `git commit -am "Some more changes"`
5. `git fetch`
6. `git push`

Person 1, again:
1. `git fetch`
2. `git log -p <branch>..origin/<branch>` see changes the coworker made to the feature branch.
3. `git merge origin/<branch>`
4. Merge changes in feature branch back to master
5. Make sure master is up to date: `git checkout master`, `git fetch`, `git merge origin/master`, or `git pull`
6. `git merge <branch>`
7. `git push`
