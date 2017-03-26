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

## Fetch - pull(download?) changes from remote
`git fetch`

## Merge - merge changes from fetch (or another branch)
In this context we're looking at fetching from a remote

Fetch before you work
Fetch before you push
Fetch often - no reason not to do it often

## Pull - pull (download?) and merge changes

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
