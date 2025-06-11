# apparmor

**Generate a starting profile:**

> Creates a profile in /etc/apparmor.d

```bash
$ aa-autodep [path-to-binary]

# eg.
$ aa-autodep /usr/bin/firefox
```

**View and edit the profile:**

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

**Load and enforce the profile:**

```bash
$ apparmor_parse -r /etc/apparmor.d/[profile]
$ aa-enforce [profile]

# eg.
$ apparmor_parse -r /etc/apparmor.d/usr.bin.firefox
$ aa-enforce /usr/bin/firefox
```

