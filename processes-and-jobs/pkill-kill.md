# pkill, kill

### pkill

* `pkill` is a utility that sends signals to the processes of a running program

Eg. To kill a process by **name**

```sh
pkill -9 <process_name>

# by exact name using regex
pkill -9 '^ssh$'
```

### kill

* Sends a specified signal to the specified processes

Eg. To kill a process by **PID**&#x20;

```sh
$ kill -9 <PID>

# eg.
$ kill -9 77372
```

### View all available signals

```sh
kill -l
 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
 6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
 ...
```
