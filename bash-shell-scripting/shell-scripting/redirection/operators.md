# Operators

## Order of redirection matters

> Note that _stdout_ (**fd 1**) is used by default if none is specified
>
> Eg. `>` is equivalent to `1>`

* The following directs both _stdout_ (fd 1) and _stderr_ (fd 2) to the file `dirlist`

```bash
ls > dirlist 2>&1 
```

* While the following directs only the _stdout_ (fd 1) to the file `dirlist`&#x20;
  * The _stderr_ (fd 2) still points to terminal (orginal value of _stdout_)

```bash
ls 2>&1 > dirlist
```

The reason being that the shell interprets the values from left to right.&#x20;

**Steps in the first example**

1. `> dirlist`: Redirect _stdout_ to `dirlist` file
2. `2>&1`: Redirect _stderr_ (fd 2) to _stdout_ (`&1`, fd 1)

* Since _stdout_ is pointing to the `dirlist` file, this points _stderr_ to that file too

**Steps in the second example**

1. `2>&1`: Redirect _stderr_ (fd 2) to _stdout_ (fd 1)

* However, since _stdout_ is currently pointing to the terminal, the _stderr_ will point to it too

2. `> dirlist`: Redirect _stdout_ to the `dirlist` file

* Overall, _stderr_ points to the terminal, while _stdout_ points to the `dirlist` file
