# environment variables

1. `$PATH`

List of directories that a system will look for when searching for executables

```bash
# eg.
$ echo $PATH
/usr/local/sbin:/usr/sbin:/sbin:/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
```

2. `$SHELL`

Indicates which shell is set as the default for the current user account

```bash
# eg.
$ echo $SHELL
/usr/bin/bash

# eg.
$ echo $SHELL
/usr/bin/zsh
```

The `$0` is a special variable that shows the currently active shell

```bash
$ echo $SHELL
/usr/bin/bash
$ echo $0 
/usr/bin/zsh

# Eg. change to /usr/bin/zsh
$ /usr/bin/zsh

# from the zsh shell
$ echo $SHELL
/usr/bin/bash
$ echo $0 
/usr/bin/zsh
```
