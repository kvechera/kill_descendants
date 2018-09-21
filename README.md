# kill_descendants

Finds and kills descendants of the processes

## Usage

```
kill_descendants [-s signal] [-t kill_timeout] [-w wait_continue] pid ...

```

## Description

The program searches all descendant processes and kills them starting from the youngest processes to let a parent process handle child's termination. The purpose of this behavior is to terminate the subtree of a process run by a script of a background command in a smooth way, similar to how a controlling terminal sends SIGINT to the foreground process group leader.

The default signal is TERM. If `kill_timeout` is set, the program sends KILL to the processes received the signal but not terminated during the timeout.

If `wait_continue` is set, the program waits the specified time for parents to handle their children's terminations, and continue to kill the parents. It keeps killing the parents of the parents and so on until no processes left or can be killed. If some childern left the program exits with code 16 and prints on stderr the pids of the processes.

## Examples

To kill all the descendants of processes with the maximal damage you can run:

```
kill_descendants -t 1 -w 1 123 456
```


## Note

It is a POSIX shell script using Linux /proc to build a process tree. It has no dependencies on other binaries.

You can use it as a library function. In this case, you should run it in a subshell to avoid variables pollution.

## Author

Kirill Vechera
http://jetware.io
2018
