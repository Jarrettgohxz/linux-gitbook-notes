# /etc/hosts, /etc/hosts.allow, /etc/hosts.deny

### /etc/hosts

The `/etc/hosts` file acts as a local database to provide information for DNS resolutions, in the form of mapping hostnames (or fully qualified domain names (FQDN)) to IP address values.&#x20;

**The following is the general format for each line in the file**

```vim
[IP_addr_to_resolve] [hostname_1] [optional_hostname_2]
```

Eg. Mapping hostname `jarrettgxz.com` to the IP address value of `8.8.8.8`

::: note

Multiple hostnames can be included for each IP address value&#x20;

:::

* The second line maps the hostnames `example.com` and `example2.com` to the IP address `10.10.10.10`.

```vim
8.8.8.8 jarrettgxz.com
10.10.10.10 example1.com example2.com 
```



### /etc/hosts.allow and /etc/hosts.deny

The /etc/hosts.allow and /etc/hosts.deny files are used to allow or restrict access to local services for specific IP addresses or hostnames.&#x20;

**General format of entry**

```vim
```



