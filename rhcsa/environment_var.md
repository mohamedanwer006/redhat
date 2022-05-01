# Variables

```bash
# define variables

name = ahmed
# integer variable
typeset -i i=0

# print to stdout
echo "Hello $name"

# print variable value $
echo $i

echo $name 

# --------------------------------------------------
# equation 
((n=5*5))
echo $n
# 25

((n=n+5))
echo $n
# 30

n=string
echo $n
# string

((n=n+20))
echo $n
#20
# string in equation equals 0
# -------------------------------------------------

```

## Environment Variables
It doesn't change the default value it show them 

```bash
# HOME home directory
echo $HOME
# USER current user 
echo $USER
# SHELL default shell
echo $SHELL
# HOSTNAME hostname

# change ENV variable will change behavior  of the command that uses them
HOME=/
cd 

pwd

#  will show /
```

```bash
# some of them will be helpful
# change prompt string number1 [user@sdf]#
PS1='mo@$PWD>'


# PATH
# contain the path for the command
echo $PATH

# -----------------------------------
mkdir ~/myscripts
cd myscripts
vi first.sh 
###
echo 'hello world!'
###


# try to run first.sh will show not found
# to way to run
# full path to first.sh or relative
# or
# add directory of my scripts  

PATH=/home/user/myscripts
# this will override all PATH 
# the changes is temporary to shell

# 
PATH=$PATH:/home/user/myscripts

# try ro run first.sh
first.sh
# echo hello world
# how to make changes permanent
# we need to save our work in files
# initialization files
# global initialization files /etc/profile changes here for all user after they login
# ~/.profile ~/.bash_profile ~/.bash_login depend on distribution
# when login first file read /etc/profile then ~/.profile 
# this file work for first login command line shell multiuser.target

# but what if need to open terminal on gui
# .bashrc work form gui or shell

# here u can add what u need to show when login in terminal
echo "hello form bashrc"
cal
##
# /etc/profile > ~/.bash_profile > ~/.bashrc

# if work on gui .bash_profile doesn't work
# best is work for .bashrc it work for gui and command line shell
# -----------------------------------

```


### show all env variable
```bash
env # print all env
printenv  # print all env
printenv  HOME  #print specific env variable with out $

man bash 
# search for variables
set 
# user variable or function or environment variable
# print all 
```

```bash
# alias  = naked name

# create alias for clear
alias c="clear"
alias #print all alias 
# remove alias
unalias c
# it temporary 
# put it in .bashrc to pe permanent
# what id name alias with the same name of command
# alias >command
# will call alias first
# full path for command
# \command 

# ignore any special meaning

# so here will call command not alias



```
