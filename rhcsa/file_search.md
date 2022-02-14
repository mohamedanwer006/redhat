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


