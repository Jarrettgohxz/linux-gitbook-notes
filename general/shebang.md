# shebang

shebang is the character sequence `#!` used at the start of a script to indicate the values that follows will be an _**interpreter directive.**_ This essentially controls which interpreter parses and interprets the instructions in the particular computer program that follows.

### Example

Given the following file named `test`

1. The contents of the `test` file is shown to contain a print statement in _**Python**_ language
2. The file executed with the `./test` command
   * An error is thrown
   * This is because the shebang is not specified. Thus, the default interpreter value (`/bin/sh`) is used.
3. To specify to the shell to use the python interpreter (`/usr/bin/python3`), the shebang needs to be included at the top of the script
4. When the script is ran again, the interpreter `/usr/bin/python3` is used.&#x20;



```bash
# 1)
$ cat test
print("hello friend")

# 2)
$ ./test
./test: line 2: syntax error near unexpected token `"hello friend"'
./test: line 2: `print("hello friend")'

# 3)
$ which python3
/usr/bin/python3

$ nano test
...

$ cat test
#!/usr/bin/python3 
print("hello world")

# 4)
$ ./test
hello friend
```
