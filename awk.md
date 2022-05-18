### Patterns to work with `awk` (Thanks to habr's post https://habr.com/ru/company/ruvds/blog/665084/)
### Useful links:
- https://likegeeks.com/awk-command/
- https://learnxinyminutes.com/docs/awk/

```bash
awk '{action}' your_file_name.txt
```
or
```bash
awk '/regex pattern/{action}' your_file_name.txt
```

#### Print all content (`$0`) from file information.txt
```bash
awk '{print $0}' information.txt
```

#### Add row number to output (`NR`)
```bash
awk '{print NR,$0}' information.txt
```

#### Print only first column
```bash
awk '{print $1}' information.txt
```

#### Print first and fourht column
```bash
awk '{print $1, $4}' information.txt
```

#### Print last column (`$NF`)
```bash
awk '{print $NF}' information.txt
```

#### Print rows that starts with leading "O"
```bash
awk '/^O/' information.txt
```

#### Print rows, that starts with ending "0"
```bash
awk '/0$/' information.txt
awk '! /0$/' information.txt # not ending with 0
```

#### Rows, that contains "io", print first column
```bash
awk ' /io/{print $1}' information.txt
```

#### Comparing column with some value
```bash
awk '$3 <  40 { print $0 }' information.txt
```

#### Column delimiter
```bash
awk -F '*' '{print $1}'
```
