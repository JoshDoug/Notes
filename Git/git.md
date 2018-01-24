# Git

*List of Git commands.*

* `git config --global branch.master.rebase true` to always rebase when pulling from master - helps [avoid those annoying merge commits](http://kernowsoul.com/blog/2012/06/20/4-ways-to-avoid-merge-commits-in-git/)
* `git config --global branch.autosetuprebase always`
* Or add an alias for `pull -rebase` in `~/.gitconfig`