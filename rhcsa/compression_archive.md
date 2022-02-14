# compression commands
1. `gzip`
2. `bzip2`

compress file
```
gzip file
```
unCompress file
```
gunzip file
```
```
bzip2 file
bunzip2 file
```


# archive directory 
archive directory
```
tar cf file.tar <directory>
```
extract archive
```
tar xf file.tar
```

archive and compress directory
```
# using tar and gzip
tar czf file.tar.gz <directory>
# using tar and bzip2
tar cjf file.tar.bz2 <directory> 
```
extract archive and decompress
```
# using tar and gzip
tar xzf file.tar.gz
# using tar and bzip2
tar xjf file.tar.bz2
```

list files in archive with out extracting
```
tar tvfz file.tar.gz
```
t = list
v = verbose
f = file
z = gzip
c = compress
x = extract
z = gzip
j = bzip2
---
 get size
 ```
 du -sh <file>
 ```
