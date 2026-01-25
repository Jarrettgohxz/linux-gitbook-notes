---
description: Curated list of useful commands for different use cases
---

# useful commands

### 1. Get PID of process

* Process with the following status:
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

### 2. Process kill signals

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

### 3. Transfer file(s) between 2 hosts

#### 3.1 Netcat

* Single file

```shellscript
# sender
$ nc <receiver_ip> <port>  < file
# receiver
$ nc -lp <port> > file
```

* Multiple files with the same extension

```shellscript
# sender
$ tar -cvf - *.ext | nc <receiver_ip> <port>
# receiver
$ nc -lp <port> | tar -xvf - 
```

#### 3.2 Secure Copy Protocol (`scp`)

> Optionally use the `-P` flag to specify the port on the remote host to connect to

* Single file

```shellscript
# transfer from remote host to local directory
$ scp <user>@<remote_host>:/path/to/source/<file> .
# transfer from local directory to remote host
 scp <file> <user>@<remote_host>:/path/to/destination/
```

* Multiple files with the same extension

```shellscript
# transfer from remote host to local directory
$ scp <user>@<remote_host>:/path/to/source/*.ext .
# transfer from local directory to remote host
$ scp *.ext <user>@<remote_host>:/path/to/destination/
```

#### 3.3 wget + Python3 server

* Single file

```shellscript
# sender
$ python3 -m http.server <port>
# receiver
$ wget http://<sender_ip>:<port>/<file> -O /path/to/output
```

