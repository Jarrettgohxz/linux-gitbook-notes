---
description: A tool that deals with .pdf files.
---

# pdftk

## pdftk

```bash
$ sudo apt install pdftk-java

# General command to extract specific pages from an input PDF file and save as 
# a new PDF file
$ pdftk <input_filename>.pdf cat [pg_start]-[pg_end] output <output_filename>.pdf

# Example: Extract page 22 from input.pdf and save to output.pdf
$ pdftk input.pdf cat 22-22 output output.pdf
```



{% embed url="https://askubuntu.com/questions/221962/how-can-i-extract-a-page-range-a-part-of-a-pdf" %}
