# chsh

The `chsh` command can be used to change a user's login shell.&#x20;

On Kali Linux version _**2024.4**_, as shown from the `lsb_release -a` command, the default login shell is `/usr/bin/zsh`. This can be verified as follows:

<pre class="language-bash"><code class="lang-bash"><strong>$ lsb_release -a
</strong>No LSB modules are available.
Distributor ID: Kali
Description:    Kali GNU/Linux Rolling
Release:        2024.4
Codename:       kali-rolling
<strong>
</strong><strong>$ echo $SHELL
</strong>/usr/bin/zsh
</code></pre>

### Example

To use the `chsh` command to change the login shell to bash (`/usr/bin/bash`).

```bash
$ which bash
/usr/bin/bash

$ chsh -s /usr/bin/bash
```

Restart the system, or simply close and reopen the terminal for the changes to be applied.
