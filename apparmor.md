# apparmor

{% embed url="https://gitlab.com/apparmor/apparmor/-/wikis/Documentation" %}

### Prerequisites

#### Ensure apparmor daemon is running

```bash
$ systemctl status apparmor
$ systemctl start apparmor
```

#### Install neccessary tools

```bash
$ apt install apparmor-utils
```

### 1. Generate a starting profile

> Creates a profile in `/etc/apparmor.d`  with the naming convention where the slashes (`/`) are converted to dots (`.`)

Eg. `/usr/bin/firefox` -> `usr.bin.firefox`

```bash
$ aa-autodep [path-to-binary]

# eg.
$ aa-autodep /usr/bin/firefox
```

### 2. Optionally, load the profile using `aa-genprof` or `aa-logprof`

> The `aa-genprof` tool uses `aa-logprof` under the hood to augment the profile

{% embed url="https://manpages.ubuntu.com/manpages/noble/en/man8/aa-logprof.8.html" %}

{% embed url="https://manpages.ubuntu.com/manpages/noble/en/man8/aa-genprof.8.html" %}

```bash
$ aa-genprof [executable] --file /path/to/logfile

# eg.
$ aa-genprof /usr/bin/firefox --file /var/log/syslog
```

### 3. View and edit the profile

```bash
$ cd /etc/apparmor.d

# /usr/bin/firefox -> usr.bin.firefox
$ vim usr.bin.firefox
abi <abi/4.0>,

include <tunables/global>

/usr/lib/firefox-esr/firefox-esr {
  include <abstractions/base>
  include <abstractions/lightdm>
  include <abstractions/postfix-common>

  capability sys_admin,

  /home/*/.cache/.mozilla/** mrixwk,
  /home/*/.cache/** mrixwk,
  /home/*/.mozilla/** mrixwk,
  /proc/** mrwk,
  /usr/lib/firefox-esr/firefox-esr mrixwk,
  /usr/lib/firefox-esr/firefox-esr mrixwk,
  /usr/lib/firefox-esr/glxtest mrixwk,
  
  deny /proc/version rwlk,

}

```

#### Abstractions

The `include <abstraction/...>` statement allows reusable profile configurations to be defined. They can be found under `/etc/apparmor.d/abstractions` .

#### Profile language

Refer to the documentation for more information on what each statement in the profile configuration mean:

{% embed url="https://gitlab.com/apparmor/apparmor/-/wikis/QuickProfileLanguage" %}

### 4. Load and enforce the profile

```bash
# Load the profile
$ apparmor_parser -r /etc/apparmor.d/[profile]
# enforce the profile
$ aa-enforce [profile]

# eg.
$ apparmor_parse -r /etc/apparmor.d/usr.bin.firefox
$ aa-enforce /usr/bin/firefox
```

### 5. View the status

```bash
$ aa-status

apparmor modules are loaded
XX profiles are loaded.
X profiles are in enforce mode.
    ...
    /usr/bin/firefox
    ...
...
    ...
```

### 6. Other commands

> Refer to the documentation link above

```bash
$ aa-disable 
$ aa-aduit
...
```

