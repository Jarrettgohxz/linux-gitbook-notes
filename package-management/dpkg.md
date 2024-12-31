# dpkg

### Install a .deb file

```bash
$ sudo dpkg -i <file>.deb
```

### View a list of installed packages &#x20;

```bash
$ sudo dpkg --list 

# list specific package by  the name
$ sudo dpkg --list | grep <installation_name>
```

### Remove an installation (from a .deb file)

```bash
$ sudo dpkg -r <installation_name>
```
