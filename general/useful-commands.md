---
description: Curated list of useful commands for different use cases
---

# useful commands

1. **Get PID of process**&#x20;

* Started with command
* Listening or established on certain service port

```shellscript
$ pgrep -a <command>
$ ps w | grep <command>
$ lsof -i4 -P -n | grep LISTENING | grep :<port>
$ lsof -i4 -P -n | grep  ESTABLISHED | grep :<port>

# eg.
$ pgrep -a ssh
$ ps w | grep ssh
$ lsof -i4 -P -n | grep LISTENING | grep :22
$ lsof -i4 -P -n | grep  ESTABLISHED | grep :22
```

2. **Common process kill signals**

```shellscript
 # SIGTERM (15) - graceful stop
 $ kill -s SIGTERM <pid>
 $ kill -SIGTERTM <pid>
 $ kill -15 <pid>
 
 # SIGKILL (9) - force kill 
 $ kill -s SIGKILL <pid>
 $ kill -SIGKILL <pid>
 $ kill -9 <pid>
 
 # SIGINT (2) - ctrl+c
 $ kill -s SIGINT <pid>
 $ kill -SIGINT <pid>
 $ kill -2 <pid>
```

3. **Transfer files between hosts**

```
```



