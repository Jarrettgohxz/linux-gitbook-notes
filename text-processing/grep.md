# grep

### Looking for text from an output

```bash
$ echo -e 'hello friend, my name \n is jarrett!'
hello friend, my name 
 is jarrett!

$ echo -e 'hello friend, my name \n is jarrett!' | grep 'name'
hello friend, my name 
```

### Search for word within a file

```bash
$ grep [word_search] [file_name]

# eg. Both lines below are equivalent, but using grep only without cat is more efficient
$ grep 'test' file.txt 
$ cat file.txt | grep 'test'
```

### Look for files in the current directory with a certain word

```bash
$ grep -irl [word_search]

# Exclude directory, and suppress errors
$ grep -irl --exclude-dir=[dir_to_exclude] [word_search] 2>/dev/null
```

#### Flags

a) `-i`:  Case-insensitive search

b) `-r`:  Perform a recursive search on the directory

c) `-l`:  Suppress normal output - only print the name of each file for which the output would have been printed from
