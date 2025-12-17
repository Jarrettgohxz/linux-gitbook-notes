# Here Doc, Here Strings

## 1. Here Doc

{% embed url="https://www.geeksforgeeks.org/linux-unix/how-to-use-here-document-in-bash-programming/" %}

### 1.1 Basic syntax

The here document (`<<`) can be used to pass a multi-line block of text or code to an interactive command

```bash
[COMMAND] << 'DELIMITER'
    HERE-DOCUMENT
DELIMITER
```

### 1.11 Example with `cat`

```bash
cat << END
'THIS BUNCH OF TEXT WOULD BE SHOWN'
END
```

### 1.12 Example with `python3`

#### Explanation of Python3 features and functions used

a. `python3 -`&#x20;

> When the script name is given as `'-'`, it refers to the standard input

{% embed url="https://docs.python.org/3/tutorial/interpreter.html?utm_source=chatgpt.com" %}

b. `sys.stdout.write`&#x20;

* Writes data to standard output (**stdout**)

{% embed url="https://docs.python.org/3/library/sys.html" %}

```bash
python3 - << 'EOF' 
print("Hello here doc!")
EOF
```

* Prints `Hello here doc!`

```bash
python3 - << 'EOF' | cat
import sys
sys.stdout.write("12345678")
EOF
```

* The _here-document_ will feed text into _stdin_ **of** `python3`&#x20;
* The pipe **(`|`**) performs the following: _stdout_ of `python3` -> stdin of `cat`
  * Prints `12345678`

```bash
python3 - << 'EOF' >> outfile
import sys
sys.stdout.write("12345678")
EOF
```

* The _here-document_ will feed text into _stdin_ **of** `python3`&#x20;
* The redirection (`>>`) will append the _stdout_ of `python3` to the file `outfile`
  * Appends `12345678` to the file

```bash
$ cat outfile
12345678
```

### 1.13 Example with while loop + read

```bash
Arr=(0 1 2 {A..D}) #  (0 1 2 A B C D)

while read element ; do
  echo "$element" 
done <<< $(echo ${Arr[*]}) 

# output: 0 1 2 A B C D
```

* Print each value in the array from &#x73;_&#x74;dout_
  * `echo` prints to the _stdout_ (**fd 1**)

<pre class="language-bash"><code class="lang-bash">Arr=(0 1 2 {A..D}) #  (0 1 2 A B C D)

while read element ; do
  echo "$element" <a data-footnote-ref href="#user-content-fn-1">1>&#x26;2</a> # >&#x26;2 works too since `>` defaults to stdout (fd 1)
done &#x3C;&#x3C;&#x3C; $(echo ${Arr[*]}) 

# output: 0 1 2 A B C D
</code></pre>

* Print each value in the array from _stderr_
  * `1>&2` redirects _stdout_ to _stderr_

<pre class="language-bash"><code class="lang-bash">Arr=(0 1 2 {A..D}) #  (0 1 2 A B C D)

while read element ; do
  echo "$element" 
done &#x3C;&#x3C;&#x3C; $(echo ${Arr[*]}) <a data-footnote-ref href="#user-content-fn-2">>> outfile</a>

# output: empty
</code></pre>

* `>> outfile` append _stdout_ to the `outfile` file
  * The file `outfile` will contain the value: **0 1 2 A B C D**

<pre class="language-bash"><code class="lang-bash">Arr=(0 1 2 {A..D}) #  (0 1 2 A B C D)

while read element ; do
  echo "$element" <a data-footnote-ref href="#user-content-fn-1">1>&#x26;2</a> # >&#x26;2 works too since `>` defaults to stdout (fd 1) 
done &#x3C;&#x3C;&#x3C; $(echo ${Arr[*]}) <a data-footnote-ref href="#user-content-fn-2">>> outfile</a>

# output: 0 1 2 A B C D
</code></pre>

* Notice that even with the `>> outfile`  command the data is not actually written to the file, but instead printed on the terminal
  * This is due to the `1>&2` command redirecting _stdout_ to _stderr_
  * The value in stderr will be printed on the terminal
* The file `outfile` will be empty

```bash
# without 1>&2
while read element ; do
  echo "$element"  
done <<< $(echo ${Arr[*]}) &>/dev/null

# output: empty

while read element ; do
  echo "$element" 1>&2
done <<< $(echo ${Arr[*]}) &>/dev/null

# output: empty
```

* Notice that the output is empty
  * This is due to the `&>/dev/null` command at the end which redirect all the _stout_ and _stderr_ to the `/dev/null` file

{% embed url="https://jarrettgxz-sec.gitbook.io/linux/general/dev-null" %}



## 2. Here Strings

{% embed url="https://www.geeksforgeeks.org/linux-unix/shell-scripting-here-strings/" %}

### 2.1 Basic syntax

&#x20;The here string (`<<<`) command is used for input redirection from a text or variable

```bash
[COMMAND] <<< 'string' # from text
[COMMAND] <<< $DATA # from variable
```

#### 2.12 Input redirection from a text

* Both commands shown below are equivalent
  * outputs `hr`

```bash
echo "here" | tr -d 'e' 
tr -d 'e' <<< "here" 
```

#### 2.13 Input redirecton from a variable

```bash
DATA="here"

echo $DATA | tr -d 'e' 
tr -d 'e' <<< $DATA 
```



[^1]: redirect stdout to stderr

[^2]: append to `outfile`
