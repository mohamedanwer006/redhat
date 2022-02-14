---
title: "get-started"
date: "2022-01-20"

---

## Linux  utilities
open tty
ctrl + alt + fn  ,  n = 2 : 6
change virtual terminal command
```
chvt <number>
```
>root id: 0
>>services id: 1 : 999
>>>users id: >= 1000


general form of command:
```
command [options] [arguments]
```
any thing between [ ] is optional
>[options] change the way the command works
>[arguments] are the things that are passed to the command


***
change user
```
su -<userName>
``` 
show user id
```
id
id <userName>
```
show date
```
date
```
show calendar
```
cal
```
show time
```
time
```
list file
```
ls
```
change directory
```
cd <directory>
```
last working directory
```
cd -
```
change directory to home
```
cd ~ <userName>
```
show current directory
```
pwd
```
create file
```
touch <fileName>
```
show file content
```
cat <fileName>
```
copy file 
```
cp <fileName> <newFileName>
```
make directory
```
mkdir <directoryName>
```
copy directory
```
cp -r <directoryName> <newDirectoryName>
```
move file
```
mv <fileName> <newFileName>
```
move directory
```
mv <directoryName> <newDirectoryName>
```
remove file
```
rm <fileName>
```
remove directory
```
rmdir <directoryName>
```
remove directory and all files
```
rm -r <DirectoryName>
```
remove recursively directory and all files 
```
rm -rf <DirectoryName>
```
change file name
```
mv <fileName> <newFileName>
```
change directory name
```
mv <directoryName> <newDirectoryName>
```
clear screen `ctrl + l`
```
clear
```

run multiple commands
```
; <command>
```

## useful shortcuts

move cursor to the beginning of the line `ctrl + a `
move cursor to the end of the line `ctrl + e `
remove to the end of the line `ctrl + k `
remove to the beginning of the line `ctrl + u `
log out `ctrl + d `
suspend `ctrl + z `
lock screen secure `ctrl + s `
unlock screen  `ctrl + q`
cancel `ctrl + c `
resume 
```
bg
```
reboot
```
reboot
shutdown -r now
systemctl reboot
init 6
```
shutdown
```

systemctl poweroff
shutdown -h now
poweroff
init 0
```
# redirections

    < input 0 

`processing`         

    1 > output 
    2 > error 

redirection of input and output
```
< input > output
< input > output 2> error
```
for example:
```
# overwrite output >
ls -l > result.txt
ls -l > result.txt 2> error.txt
ls -l > result.txt 2>&1
# append output >>
ls -l >> result.txt
# append output and error
ls -l >> result.txt 2>&1
ls -l 2&> result.txt
```
input redirection
```
cat <<EOT>> output
some text
EOT
```
pipe | pass output to the second command
```
ls -l / | less
```
use tee
```
ls -l / | tee result.txt
```
get file extension
```
file <fileName>
```
# simple command
# wh command

quick summary of every user logged into a computer

```
w
who
```
```
whatis <command>
whereis <command>
last
lastlog

```
get total size of all files in a directory
du -sh = disk usage summary human readable  
```
du -sh <directory>
```

\ called escape character
```
#create two file mohamed and anwer 
touch mohamed anwer
#create one file mohamed anwer 
touch mohamed\ anwer
```

use Alt + d
on booting to show logs screen

any file system mounted on system 

is on /etc/mtab
```
cat /etc/mtab
```



