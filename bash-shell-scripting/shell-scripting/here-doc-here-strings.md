# Here Doc, Here Strings

## 1. Here Doc

{% embed url="https://www.geeksforgeeks.org/linux-unix/how-to-use-here-document-in-bash-programming/" %}

### 1.1 Basic syntax

The here document (`<<`) can be used to pass a multi-line block of text or code to an interactive command

```bash
[COMMAND] << 'DELIMITER'
    HERE-DOCUMENT
DELIMITER

# eg.
[COMMAND] << 'END'
    HERE-DOCUMENT
END
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

> When the script name is given as `'-'`, it refers to the standard input          &#x20;

{% embed url="https://docs.python.org/3/tutorial/interpreter.html?utm_source=chatgpt.com" %}

b. `sys.stdout.write`&#x20;

* Writes data to standard output (**stdout**)

{% embed url="https://docs.python.org/3/library/sys.html" %}

#### Example 1

```bash
python3 - << 'EOF' | cat
import sys
sys.stdout.write("12345678")
EOF
```

* Simply prints `12345678`

#### Example 2

```bash
python3 - << 'EOF' >> outfile
import sys
sys.stdout.write("12345678")
EOF
```

* Simply appends `12345678` to the output file `outfile`

```bash
$ cat outfile
12345678
```

## 2. Here Strings

{% embed url="https://www.geeksforgeeks.org/linux-unix/shell-scripting-here-strings/" %}

### 2.1 Basic syntax

&#x20;The here string (`<<<`) command is used for input redirection from a text or variable

```bash
[COMMAND] <<< 'string'
[COMMAND] <<< $DATA
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

