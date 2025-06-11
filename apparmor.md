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



### Default firefox profile shipped with Kali Linux

```vim
# This profile allows everything and only exists to give the
# application a name instead of having the label "unconfined"

abi <abi/4.0>,
include <tunables/global>

profile firefox /{usr/lib/firefox{,-esr,-beta,-devedition,-nightly},opt/firefox}/firefox{,-esr,-bin} flags=(unconfined) {
  userns,

  # Site-specific additions and overrides. See local/README for details.
  include if exists <local/firefox>
}

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

> usr.bin.firefox

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

#### Generate a new profile according to logs from the specified log file

> For `/usr/bin/firefox`, I used `aa-autodep` instead of `aa-genprof` to generate the starting profile. This is because there are too many file reads from firefox (as shown in the log file), thus `aa-genprof` displays too much output.

```bash
$ aa-genprof [executable] --file /path/to/logfile

# eg.
$ aa-genprof /usr/bin/firefox --file /var/log/syslog
```

#### Update the existing profile

```bash
$ aa-logprof --file /path/to/logfile

# eg.
$ aa-logprof --file /var/log/syslog
```



### 3. View the profile and manually edit the configurations

```bash
$ cd /etc/apparmor.d

# /usr/bin/firefox -> usr.bin.firefox
$ vim usr.bin.firefox

# ********************************
# ** My current profile

abi <abi/4.0>,

include <tunables/global>

profile firefox /{usr/{bin,lib/firefox{,-esr}},opt/firefox}/firefox{,-esr,-bin}

{
  userns,
  
  #include <abstractions/base> # seems to not be required

  # ~~~~~~~~~~~~~~~~~~~~~
  # ALLOW FIREFOX-ESR FILES
  # ~~~~~~~~~~~~~~~~~~~~~
  /usr/lib/firefox-esr/firefox-esr ix,
  /usr/lib/firefox-esr/glxtest ix,
  /usr/lib/firefox-esr/minidump-analyzer ix,

  # ~~~~~~~~~~~~~~~~~~~~~
  # ALLOW HOME DIR FILES
  # ~~~~~~~~~~~~~~~~~~~~~
  @{HOME}/.local/share/** wrmkix,
  @{HOME}/.config/** wrmkix,
  @{HOME}/.cache/.mozilla/** r,
  @{HOME}/.mozilla/** rwmkix,
 
  # ~~~~~~~~~~~~~~~~~~~~~
  # ALLOW OTHER FILES - to refined: make the file accesses more fine-tuned
  # ~~~~~~~~~~~~~~~~~~~~~
  owner /tmp/** rwkmix, 
  /tmp/firefox-esr/** rwkmix,
  
  /etc/** r,
  /proc/** rw,
  /usr/share/** r,
  /usr/local/share/** r,
  /var/cache/fontconfig/** r,
  /sys/** r,
  /var/** r,
  /dev/** rw,
  owner /run/user/@{uid}/** rw, # owner keyword
  
  # ~~~~~~~~~~~~~~~~~~~~~
  # DENY
  # ~~~~~~~~~~~~~~~~~~~~~
  deny /etc/ssh/** rwkmx,

  # ~~~~~~~~~~~~~~~~~~~~~
  # CAPABILITY
  # ~~~~~~~~~~~~~~~~~~~~~
  capability sys_admin,
  capability sys_chroot,

  # ~~~~~~~~~~~~~~~~~~~~~
  # NETWORK
  # ~~~~~~~~~~~~~~~~~~~~~
  # network netlink raw, # ~raw sockets - requested by Firefox, but not neccessary
  network inet dgram, # UDP
  network inet stream, # TCP

  # Site-specific additions and overrides. See local/README for details.
  include if exists <local/firefox>
}

 
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

### 6. View the logs and manually update the profile

After loading the profile into the kernel, we can run the application (controlled by `apparmor` in **enforce** mode), and view the logs for any _DENIED_ error messages:

#### Install required packages

```bash
$ apt install rsyslog
$ systemctl start rsyslog

```

#### Filter the logs

```bash
$ cat /var/log/syslog | grep [executable]  | grep -P T[timestamp]\w* 

# eg. firefox at 1800 HRS
$ cat /var/log/syslog | grep firefox  | grep -P T18:\w* 
$ cat /var/log/syslog | grep firefox  | grep DENIED | grep -P T18:\w* # view DENIED 
```

#### View the logs in real-time

```bash
$ tail -f /var/log/syslog | grep -E 'firefox|DENIED' 
```

From the error messages, we can update the profile linked to the executable accordingly.

#### Example

Given the following error message:

{% code overflow="wrap" %}
```log
xxxx : apparmor="DENIED" operation="open" class="file" profile="firefox" name="/proc/xxxx/xxxx" ... comm="firefox-esr" requested_mask="w" denied_mask="w" 
```
{% endcode %}

The message tells us that `firefox-esr` is trying to write (`w`) to `/proc/xxxx/xxxx`, but got _DENIED_ access. To fix this issue, we can add a rule to the profile:

```vim
/proc/** w,
```

For more information on file pattern matching, refer to the documentation on the _**File Globbing**_ section:

{% embed url="https://gitlab.com/apparmor/apparmor/-/wikis/QuickProfileLanguage" %}

### 7. Verify the apparmor configurations

...

#### Example

Given the configurations in place for firefox, we can now open up a window and check if the file restrictions are working.

...

### 8. Other useful commands

> Refer to the documentation link at the start of this page

```bash
$ aa-disable 
$ aa-audit
...
```

