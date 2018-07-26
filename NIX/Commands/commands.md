# List of Commands with examples

Any command sufficiently complex *cough* GREP *cough*, will/should be broken out into its own file.

* ls
* stat
* file
* [`pidof`](https://linux.die.net/man/8/pidof) - find the process ID of a running program

## wget

* `wget -c http://example.com` - [resume a stalled download](https://www.garron.me/en/bits/wget-resume-continue-broken-download.html)

## Jobs

Jobs, aka tasks or processes, can be managed in several ways on Linux/Unix using the Bash shell, or ZSH and KSH (and more). This will focus on Bash syntax that may or may not work in other shells.

Running a process in the background: `task &`, by adding the ampersand the task is run in the background and a user can still interact with the prompt. When a task is run in the background two pieces of informtation are provided, typically in the form `[1] 4867`, where the first number in brackets is the job number, and the second number is the process Id. When the process is finished some additional information is returned: `[1]+ Done`, the task is finished and the process no longer exists so 'Done' is returned instead, the plus, `+`, refers to the most recent process sent to the background. A minus, `-`, refers to the previously backgrounded process.

A process can be temporarily suspended with the shortcut `C-z`, and resumed with the command `fg`. To start a suspended process in the background use the background command and the job number: `bg %1`, the most recently suspended process can be resumed in the background with just `bg`. Multiple jobs can be specified like so: `bg %4 %5`.

Bringing a background process into the foreground can also be done with the foreground command and specifying the job number: `fg %1`, resuming a process with just `fg` will only work if it was the last process to be suspended/run in the background (? need to clarify TKTK), and `fg -` to resume the second most recently backgrounded process. While `%1` on its own works in bash, `fg %1` is more consistent with other shells.

To terminate a foreground process: `C-c`. To stop/suspend a background task: `kill -STOP 4867`, where the number of the process is the process Id. Alternatively the job number can be used instead: `kill -STOP %1`.

Using the `kill` command a job can be interupted, stopped, and more, but also resumed: `kill -CONT 5294` would continue the job associated with that process Id.

The jobs command, `jobs`, provides information about currently running jobs. The `jobs` command is builtin so the `help` command is used instead of the `man` command to access usage information. To list the process Ids of a job use the l flag: `jobs -l`.

A job can be removed from the jobs list with the `disown` command which can allow a job to run beyond the current session, although there isn't a way to reposses a disowned process.