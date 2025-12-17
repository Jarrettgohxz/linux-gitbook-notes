# stdin, stderr, stdout

## 1. `stdin`

* File descriptor **0**

## 2. `stdout`

* File descriptor **1**

## 3. `stderr`&#x20;

* File descriptor **2**

## 4. `&>`&#x20;

* **Bash-specific** shortcut: indicates redirection for both _stdout_ and _stderr_

```bash
command &> file.txt # bash specific
command > file.txt 2>&1 
```

*   Both commands redirects both _stdout_ and _stderr_ from `command` to the `file.txt` file

    * The first command uses the bash-specific `&>` redirection operator
    * For other shell (eg. zsh, dash etc.) we have to use the more formal syntax indicated in the second line

    > Note that `>` can be replaced with `1>` too
