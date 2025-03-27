# find

**Basic command overview:**

To search for files within a directory hierarchy

```bash
$ find <start_directory> [flags]
```

To search from the current directory, use a period `.` as the start directory

```bash
$ find . [flags]
```

To search from the root directory (`/`)

```bash
$ find / [flags]

# eg.
$ find / -name flag.txt 
```

#### Permission denied error message

Sometimes there may be an error message returned similar to the following:&#x20;

`find: ‘/...’: Permission denied`

Simply append `2>/dev/null` at the end of the command:

```bash
# 2>/dev/null redirects all errors to /dev/null. This essentially 
# flushes all the errors away
$ find ... 2>/dev/null
```



<mark style="color:green;">Useful flags</mark>

**-name**

To find by base of filename, with the leading directories removed. The `-path` flag discussed below can be used instead if leading directories searches are required

```bash
$ find <start-dir> -name [pattern]

# eg. 
$ find . -name 'pattern'
$ find . -name '*pattern*'
```

**-path**

The `-path`flag allows matching of forward slash characters (/). This can allow searching within sub-directories of folders

```bash
$ find <start-dir> -path [pattern]

# eg. 
$ find . -path '*pattern*'
```

The asterisk (\*) in the search pattern for -name and -path flags are used for wildcard matching. To illustrate ...

```bash
$ ...
```

<mark style="color:purple;">**Difference between -name and -path**</mark>

<pre class="language-bash"><code class="lang-bash"><strong># Example file directory
</strong><strong>user@linux~/$ ls
</strong>test-dir test-dir2 

# test-dir2 contains a .txt file (random.txt) - the rest are empty
user@linux~/$ ls test-dir2
random.txt

#
# Example difference between -name and -path flags
#

user@linux~/$ find . -name 'test-dir*'
./test-dir
./test-dir2


user@linux~/$ find . -path '*test-dir*' 
./test-dir
./test-dir2
./test-dir2/random.txt


user@linux~/$ find ~ -name 'test-dir*'
/home/user/test-dir
/home/user/test-dir2


user@linux~/$ find ~ -path '*test-dir*' 
/home/user/test-dir 
/home/user/test-dir2
/home/user/test-dir2/random.txt
</code></pre>

**-type**

To search by file type ...

**-perm**

To search files by permissions ...

owner-group-users -> rwxrwxrwx -> 111 111 111 -> 777 (?)&#x20;



excerpt from [https://man7.org/linux/man-pages/man1/find.1.html](https://man7.org/linux/man-pages/man1/find.1.html)

```
   Searching files by permissions
       •      Search for files which are executable but not readable.

                  $ find /sbin /usr/sbin -executable \! -readable -print

       •      Search for files which have read and write permission for
              their owner, and group, but which other users can read but
              not write to.

                  $ find . -perm 664

              Files which meet these criteria but have other permissions
              bits set (for example if someone can execute the file)
              will not be matched.

       •      Search for files which have read and write permission for
              their owner and group, and which other users can read,
              without regard to the presence of any extra permission
              bits (for example the executable bit).

                  $ find . -perm -664

              This will match a file which has mode 0777, for example.
```

