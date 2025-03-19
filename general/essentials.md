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

