# Web fuzzing

1. POST request fuzzing

* Fuzzing a payload list of request body data

```bash
#!/usr/bin/bash
TARGET="https://<arget>"
ENDPOINT="/endpoint/xxxx"
COOKIE="xxxx=xxxx"

payloads=(
'{"xxxx":"xxxx","xxxx":"xxxx"}'
'{"xxxx":"xxxx","xxxx":"xxxx"}'
)

for p in "${payloads[@]}"; do
  echo "=== Trying payload === $p"

  http_code=$(curl -w "%{http_code}" -s -o /dev/null -X POST "$TARGET$ENDPOINT" \
    -H "Cookie: $COOKIE" -H "Content-Type: application/json" -d "$p")
  if [[ "$http_code" != "400" ]]; then
    echo ">>> Non-400 response: $http_code"
    echo "SUCCESS"
    exit
  else
    echo "-> 400"
  fi
done
```

_**cURL options**_

a. `-w/--write-out`&#x20;

* `http_code`:&#x20;
  * A variable available to the `-w/--write-out` flag
  * Displayed in the format: `%{variable}`
  * Indicates the "_The numerical response code that was found in the last retrieved HTTP(S) or FTP(s) transfer_" (eg. 200, 400, 403, etc.)

b. `-s`: Silent or quiet mode

c. `-o /dev/null`: Discard output

* Refer to the cURL manpage for more info: [https://linux.die.net/man/1/curl](https://linux.die.net/man/1/curl)
