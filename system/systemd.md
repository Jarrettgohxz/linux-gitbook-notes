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
