# file search
1. locate
2. find

## locate
### depend on database
```
locate <fileName>
```
update db
```
updatedb
```
## find
### find file in current directory
```
find . -name <fileName>
find -name <fileName>
find <path> -name <fileName>
```
find on any directory
```
find <path> -name <fileName>
```
search on permission
```
find <path> -perm <permission>
find /etc/ -pem 755
```
search on size
```
find <path> -size <size>
```
search on group
```
find <path> -group <groupName>
```
search on user
```
find <path> -user <userName>
```
search on time
```
find <path> -atime <time>
```

find /etc/ -inam network -exex cp {} work/ \;
```
[root@server -1# find /var -iname log -exec cp -r {} work/
find: missing argument to
[root@server -]#
[root@server -j#
[root@server -1#
[root@server ~]# date;ls 
```
`-exec` used for execute another command after find command is done
`-exec <command> {} \;`
`{}` used to data from find command
`\` used as escape character for ` ;`

# search content of file
## using grep command
```
grep <searchWord> <fileName>
```
search inverse 
```
grep -v <searchWord> <fileName>
```
v => inverse
i => ignore case
n => print line number
R => recursive search
l => file name only

## search using cut command

```
cut -d <delimiter> -f <fieldNumber> <fileName>
cut -d : -f 1 /etc/passwd
cut -d : -f 1-3 /etc/passwd
cut -d : -f 1-3,5 /etc/passwd
cut -d : -f 1,3 /etc/passwd
```
sort search
```
sort
```
```
cut -d : -f 3 /etc/passwd |sort -n
```
n => numeric

get unique value from file
```
cut -d : -f 7 /etc/passwd |sort|uniq
```
`uniq` make compare value  with next value and remove duplicate value
so we use `sort` to sort value and ` uniq `to remove duplicate value


## Redirection

default redirection is to stdout screen

default redirection is to stdin keyboard

### file descriptor
- #### 0 stdin
- #### 1 stdout
- #### 2 stderr

```bash 
# output redirection
# > file
ls > file.txt
# if file exist will overwrite it
# if file not exist will create it

# append redirection
# >> file
ls >> file.txt
# if file exist will append to it
# if file not exist will create it


# input redirection
< file


# error redirection
ls 2> file.txt
# if file exist will overwrite it
# if file not exist will create it

# redirect both
ls -R / > file1.txt 2> file5.txt


```

### pipe
```bash
ls | grep .sh
# will show all .sh files
```

### tee
```bash
# pipe
# |
ls -R / |tee file1.txt |less
```

### word count
```bash
wc /etc/passwd
# will show number of lines
# number of words
# number of characters

# show number of line
wc -l /etc/passwd
# show number of words
wc -w /etc/passwd
# show number of characters
wc -c /etc/passwd

wc -l < file.txt # read from file

```

### diff
```bash
diff file1.txt file2.txt
# will show the difference between file1.txt and file2.txt
# 2c2 # c for change between line 2 in file 1 and line 2 in file 2
# 1a2 # a for add or append line 2 in file 2 in file 1
# 2d1 # d for delete line 2 in file 1
```

## grep
```bash
grep -i hello file.txt
# will show all lines that contain hello in file.txt
# -i ignore case
grep nc /etc/passwd
# search as pattern
# will show all lines that contain nc in passwd
grep -w nc /etc/passwd
# search as word
# will show all lines that contain nc word in passwd
grep bash /etc/passwd
# 
grep -v bash /etc/passwd
# will show all lines that not contain bash in passwd
# -v is inverse or not


## count users have bash
grep -c bash /etc/passwd
#-c count

greps -n mohamed /etc/passwd
# -n number
# will show number of line

grep -l mohamed /etc/passwd /etc/group
# -l list
# will show file if it contain mohamed

```
## tr 

```bash
tr a b
# will replace all a with b
echo Hello World | tr 'a-z' 'A-Z'
# will print HELLO WORLD
```
### cut
```bash
cut -d: -f1 /etc/passwd
# -d delimiter
# -f field
cut -d: -f1,3 /etc/passwd

``` 

## sort
```bash

sort -t: -k3 /etc/passwd
# -t delimiter
# -k field
# sort by field 3
sort -t: -k3 -n /etc/passwd
# sort by field 3 and number

```
