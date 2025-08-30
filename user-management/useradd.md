# useradd

{% embed url="https://man7.org/linux/man-pages/man8/useradd.8.html" %}

> useradd - create a new user or update default new user information

### Example

Suppose we want to create a user named `tunneluser` that is used primarily to accept SSH  connections (eg. for tunneling, etc.). This user should have no access to the shell console.

```shell
useradd tunneluser -m -d -/home/tunneluser -s /bin/true
# or 
useradd tunneluser --create-home --home-dir /home/tunneluser --shell /bin/true
```

* `-m/--create-home` : create the user's home directory if it does not exit
* `-d/--home-dir HOME_DIR` : the new user will be created using **HOME\_DIR** as the user's login directory
* `-s/--shell` : sets the path to the user's login shell
  * the value `/bin/true` simply returns true by doing nothing, successfully
  * this is useful to prevent remote users who connects via SSH, from accessing the shell and perform actions such as file transfers ([SCP](https://jarrettgxz-sec.gitbook.io/networking-concepts/ssh/scp-sftp)) or command execution.

{% embed url="https://man7.org/linux/man-pages/man1/true.1.html" %}



