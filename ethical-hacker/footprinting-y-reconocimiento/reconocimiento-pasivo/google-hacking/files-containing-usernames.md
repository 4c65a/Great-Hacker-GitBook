---
description: https://www.exploit-db.com/google-hacking-database?category=1
---

# Files Containing Usernames

```
allintext:username filetype:log
```

```
intitle:"index of" "/usernames"
```

```
intext:"-----BEGIN CERTIFICATE-----" ext:txt
```

```
intitle:"index of" "contacts.txt"
```

```
intitle:"index of" "db.properties" | "db.properties.BAK"
```

```
intitle:"index of" "credentials.xml" | "credentials.inc" | "credentials.txt"
```

```
intitle:"index of" "credentials.xml" | "credentials.inc" | "credentials.txt"
```

```
intitle:"index of" "password.yml
```

```
"'dsn: mysql:host=localhost;dbname=" ext:yml | ext:txt "password:"
```

```
filetype:csv intext:"Secret access key"
```

```
inurl:user intitle:index of ext:sql | xls | xml | json | csv
```

```
jdbc:mysql://localhost:3306/ + username + password ext:yml | ext:java -git -gitlab
```

```
intitle:"index of" "/parameters.yml*"
```

```
"authentication failure; logname=" ext:log
```

```
inurl:"/root/etc/passwd" intext:"home/*:"
```

```
intext:"root:x:0:0:root:/root:/bin/bash" inurl:*=/etc/passwd
```

```
intitle:"index of" "users.sql"
```

```
intitle:"index of" "/ftpusers"
```

```
intitle:index.of .bash_history
```

```
intitle:index.of .sh_history
```
