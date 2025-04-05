# systemd

To add a `systemd` service, simply add a file with the `.service` extension in the `/etc/systemd/system` directory.

**Basic systemd service configuration file**:

```systemd
[Unit]
Description=[description]
After=network.target  # Script runs after the network is UP

[Service]
ExecStart=/path/to/script.sh
Restart=always  # Script will restart if it fails
User=root # run as the root user

[Install]
WantedBy=multi-user.target  # Services start at boot
```

The script `/path/to/script.sh` will be executed by the _**root**_ user after the network is UP.

**Start the service**

```bash
systemctl daemon-reload
systemctl enable [name_of_service].service
```

### Common errors

1. `ExecStart`&#x20;

* Script path not found
* Script is not executable
* Script does not contain shebang (`#!`) — alternatively, include shell path before the script path&#x20;

> Eg. `/bin/bash /path/to/script.sh`
