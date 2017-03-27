# Using local and remote repositories, and branches

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

## Fetch - download changes from remote (but don't merge them)
`git fetch`

## Merge - merge changes from fetch (or another branch)
In this context we're looking at fetching from a remote

Fetch before you work
Fetch before you push
Fetch often - no reason not to do it often

You want to switch to the branch (typically master) that will receive the merged changes. So if you're on a feature branch and you want to merge that feature back into master, then switch to master, `git checkout master` and merge: `git merge feature_branch`

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

## Pull - fetch and merge changes

## Branches
Does this make sense in this file? Not really.

* `git branch` view branches (but not remotes)
* `git branch newbranch` creat a new branch called newbranch
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
