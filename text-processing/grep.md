# grep



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
