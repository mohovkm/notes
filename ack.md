### Find all matches for usage of `\Aws\{module}\{another}` and print only capturing group
```
ack '([\\]?Aws\\.+?(?=[;|\n|(|:| |}|)]))' . -o -h | sort -u
```

