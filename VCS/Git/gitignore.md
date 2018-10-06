# Using .gitignore
The .gitignore file is used to tell git which files to use for commits and which to ignore. Useful for ignoring binary files you don't want to store in git, and files produced during the build process such as jars, compiled classes, and downloaded dependencies.

Certain files can be specified, or regex (in this case very basic regex, reduced to mainly wildcards) can be used to ignore a more generic range of files, e.g. `*.class` to ignore any compiled java bytecode.

## Examples
Ignore all files in a directory with a trailing slash: `build/`

## Comments
`# Just use a hash to create a comment`

## Negate expressions with `!`
What if you have several properties file and you want to ignore all of them, maybe they contain passwords, but there is a single exception, a properties file that you do want to track. Well this can be done like so:

* `*.properties`
* `!mandatory.properties`

The negation expression is like a double negative. (?)

## Configure git to globally ignore files
Tell git where you want to put the global ignore file, and what it is called (it doesn't have to be called .gitignore_global but it makes sense to call it that). When installing GitHub Desktop it will place this in ~/.config/git/ignore

`git config --global core.excludesfile ~/.gitignore_global`

## Ignoring tracked files
 Useful if you want to provide a placeholder log file for everyone that clones the repo without the newly logged contents of the log file being available to commit for everyone.

`git rm --cached examplefile.txt`
This removes the file from staging (?), but leaves it in the repo and working directory. Doesn't need to be staged or anything to do this. Just needs to have been previously committed.

## Tracking empty directories
Git doesn't track empty directories by default.

Tracking empty directories can be useful if a project expects a directory to exist (maybe it should just check first and create it..but who cares).

So put a file in there, called .gitkeep (by convention, but name doesn't really matter).

## GitHub Resources for ignoring files:
https://help.github.com/articles/ignoring-files/

https://github.com/github/gitignore
