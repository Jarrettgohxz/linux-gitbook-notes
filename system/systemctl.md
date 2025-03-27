# systemctl

### Control system process/daemons

```bash
$ systemctl stop [process/daemon]
$ systemctl start [process/daemon]
$ systemctl restart [process/daemon]
$ systemctl status [process/daemon]
```

#### Examples

```bash
$ systemctl stop sshd.service
$ systemctl stop networking.service
$ systemctl stop ...
```
