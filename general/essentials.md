---
description: >-
  In this section, I  will be discussing some basic Linux commands, along with a
  few basic flags associated with each commands. The term flag refers to the
  arguments/parameters supplied to the command.
---

# essentials

apt, apt-get, file, diff

### ls&#x20;

Lists contents in specified directory. If **\<dir>** value is omitted, the current directory would be used instead

```bash
$ ls <dir>
Desktop Downloads Documents 
Public Pictures ...

```

<mark style="color:green;">Useful flags</mark>

**-l**

To display content in long listing format

```bash
$ ls -l 
```

**-a, --all**

To display all content including those starting with . (hidden files)

```bash
$ ls -a 
```

Combination of multiple flags

* Display all content including hidden files (starting with .), in long listing format

```bash
$ ls -la 
```

### pwd

To print the current working directory

```bash
user@linux:~/$ pwd
/home/user
```

### cd

To change directory

```bash
$ cd <dir>
```

Basic example

```sh
# print the current working directory
user@linux:~/$ pwd
/home/user

# change directory
user@linux:~/$ cd test_dir

# pwd displays the updated directory
user@linux:~/test_dir$ pwd
/home/user/test_dir
```

### mkdir

To create a new directory

```bash
$ mkdir <new_dir>

# example
user@linux:~/$ mkdir test_dir
user@linux:~/$ cd test_dir
user@linux:~/test_dir$ 
```

### cat

From manpage: "concatenate files and print on standard output". In simple terms, it displays the content of a particular input file

```bash
$ cat test_file.txt
here is a test file
next line here
```

<mark style="color:green;">Useful flags</mark>

**-n, --number**&#x20;

To display output line numbers

```bash
$ cat -n test_file.txt
1 here is a test file
2 next line here

$ cat ---number test_file.txt
1 here is a test file
2 next line here
```

### find

To search for files within a directory hierarchy

```bash
$ find <start_directory> [flags]
```

To execute from current directory, use a period . as the start directory

```bash
$ find . [flags]
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

### locate



