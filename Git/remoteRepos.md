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

* `git branch`
* `git branch -r` lists remote branches
* `git branch -a` lists all branches
