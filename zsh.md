Zshell stuff
============

Prefix/postfix for each file in a glob
--------------------------------------

Example:

```
# touch file{1..3}
# ls
file1  file2  file3
# print ./sample-command *(P:-f:)
./sample-command -f file1 -f file2 -f file3
# print ./sample-command *(P:--pre1:^P:--post:^P:--pre2:)
./sample-command --pre1 --pre2 file1 --post --pre1 --pre2 file2 --post --pre1 --pre2 file3 --post
# print ./sample-command *(P:--pre:^P:--post1:P:--post2:)
./sample-command --pre file1 --post1 --post2 --pre file2 --post1 --post2 --pre file3 --post1 --post2
```

