# Linux Process management

> kernel control process with process id = PID

process  pages

first precess start on redhat is systemd on rh7
on rh6 it is init
PID for systemd si 1

### get running process 
```
ps
```
### get running process on all terminal
```
ps a
```
### get running process on system with full information
```
ps aux

```
### get running process on system with PPID
```
ps -ef
```
```
pstree
```
kill process 
```
kill <pid>
```
by default kill process will send signal 15 (signal terminate)
list all kill signal 
```
kill -l
```
process search
```
pgrep <processName>
```
```
pkill <processName>
killall <processName>
```
run process in background
```
<appName> &
```

ctrl+z to pause process
ctrl+c to kill process

### get running jobs
```
jobs
```

run in background
```
bg %<jobNumber>
```
run in foreground
```
fg %<jobNumber>
```
control process priority 40 point scale  => nice value -20 to 19
default priority is 0 (normal)
-20 is the highest priority
19 is the lowest priority

normal user can give low priority to process not high

```
nice -n <value> <processName>
nice <value> <processName>
```
## change priority of process
```
renice -n <value> <pid>
```

## list realtime running process with top command 

```
top 
```
use k to kill process
use q ro quit



## useful tools
sar to monitor system resource usage
rrdtool to generate graph
gnuplot to generate graph

