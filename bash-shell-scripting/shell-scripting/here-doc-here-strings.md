# Here Doc, Here Strings

## 1. Here Doc

```
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

