# firejail

```bash
$ firejail [application] [options]
```

Eg. Firefox

```bash
$ firejail firefox --net=eth0 # suppose we have a default interface named eth0
```

* `--net=eth0`:

Restrict network access to the `eth0` interface. To allow this option for regular (non-root) users, we have to comment out the `restricted-network yes` line  in the `/etc/firejail/firejail.config` file:

{% code overflow="wrap" %}
```vim
# Restricted networking grants access to --interface, --net=ethXXX and --netfilter only to root user. Regular users are only allowed --net=none
restricted-network yes # comment out this line to remove the restrictions for regular users
```
{% endcode %}

Suppose we have a simple web server running on localhost port 8888:

```bash
$ python3 -m http.server 8888
```

Usually, accessing http://localhost:8888 from the web browser will return the directory listing from which the server is running. However, if we supply the option `--net=eth0` to the _firejail_ command when running the web browser (eg. firefox), the access will be blocked, and we will receive an error when trying to access the address.

This is because we access the localhost address via the loopback (`lo`) interface, which has not been allowed.

### Examples

1. Safe document viewer&#x20;

{% embed url="https://jarrettgxz-sec.gitbook.io/offensive-security-concepts/safe-document-viewer/pdf" %}
