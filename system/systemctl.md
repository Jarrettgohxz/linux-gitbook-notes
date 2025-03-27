# systemctl

### Controlling systemd services and daemons

```bash
$ systemctl stop [service/daemon]
$ systemctl start [service/daemon]
$ systemctl restart [service/daemon]
$ systemctl status [service/daemon]
$ systemctl enable [service/daemon]
$ systemctl disable [service/daemon]
```

#### Examples

```bash
$ systemctl stop sshd.service
$ systemctl stop networking.service
$ systemctl stop ...
```
