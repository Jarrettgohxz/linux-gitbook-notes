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

#### Default profile

> Generated on Kali Linux (Kali 6.12.25-1kali1 (2025-04-30))

```vim
abi <abi/4.0>,

include <tunables/global>

/usr/bin/firefox flags=(complain) {
  include <abstractions/base>
  include <abstractions/bash>

  /usr/bin/dash ix,
  /usr/bin/firefox r,

}
```

### 2. Optionally, load the profile using `aa-genprof` or `aa-logprof`

> The `aa-genprof` tool uses `aa-logprof` under the hood to augment the profile

{% embed url="https://manpages.ubuntu.com/manpages/noble/en/man8/aa-logprof.8.html" %}

{% embed url="https://manpages.ubuntu.com/manpages/noble/en/man8/aa-genprof.8.html" %}

#### Generate a new profile according to logs from the specified log-file

> For /usr/bin/firefox, I used `aa-autodep` instead of `aa-genprof` to generate the starting profile. This is because there are too many file reads from firefox (as logged in the log-file), thus `aa-genprof` requires too much output.

```bash
$ aa-genprof [executable] --file /path/to/logfile

# eg.
$ aa-genprof /usr/bin/firefox --file /var/log/syslog
```

#### Update the existing profile

```bash
$ aa-logprof --file /path/to/logfile

# eg.
$ aa-logprof-file /var/log/syslog
```



### 3. View and edit the profile

```bash
$ cd /etc/apparmor.d

# /usr/bin/firefox -> usr.bin.firefox
$ vim usr.bin.firefox

# ********************************
# ** my current profile

abi <abi/4.0>,

include <tunables/global>

profile firefox /{usr/{bin,lib/firefox{,-esr}},opt/firefox}/firefox{,-esr,-bin}

{
    
  userns,

  include <abstractions/base>
  #include <abstractions/lightdm>
  #include <abstractions/postfix-common>
  # include <abstractions/bash>

  #/usr/bin/dash ix,i
  #/usr/bin/firefox rix,
  #/usr/lib/firefox-esr/firefox-esr rix,

  #capability sys_admin,

  @{HOME}/.local/share/** wrmkix,
  @{HOME}/.config/** wrmkix,
  @{HOME}/*/.cache/.mozilla/** r,
  @{HOME}/.cache/** wrmkix,
  @{HOME}/.mozilla/** rwmkix,
 #/proc/** w,
 
  /home/jarrettgxz/.mozilla/firefox/0le77730.default-esr/extensions/** rwkix,

  #/home/*/.cache/.mozilla/** mrixwk,
  #/home/*/.cache/** mrixwk,
  #/home/*/.mozilla/** mrixwk,
  #/proc/** mrwk,
  #/usr/lib/firefox-esr/firefox-esr mrixwk,
  #/usr/lib/firefox-esr/firefox-esr mrixwk,
  #/usr/lib/firefox-esr/glxtest mrixwk,
 
  # deny /proc/version rwlk,

}
# ********************************

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

#### apparmor\_parser

Used to compile the profile (understood by the kernel), and load it into the kernel

* `-r` flag: To update the existing profile in the kernel

> This flag is required if an AppArmor definition by the same name already exists in the kernel; used to replace the definition already in the kernel with the definition given on standard input.

{% embed url="https://manpages.ubuntu.com/manpages/lunar/man8/apparmor_parser.8.html" %}

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

