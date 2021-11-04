- ###  forgot to start the job in tmux or screen? no problem; do this:
```
0- put in bg (skip if you already used &)
1- get pid from jobs -l (or jobs -p if you happened to be running only one job at the same time)
2- disown $PID
3- screen -S lol
4- reptyr $PID
5- ^A d (detach)
6- enjoy the peace of mind
```
