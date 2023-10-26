---
description: https://www.exploit-db.com/google-hacking-database?category=1
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Footholds

```
inurl:adminpanel site:gov.*
```

```
intitle:"index of" "httpd.pid"
```

```
intitle:"index.of" +jmx-console
```

```
intitle:"Index of /" +.htaccess
```

```
intitle:"index of" "nginx.log"
```

```
inurl:"/arcgis/rest/services"
```

```
"radius-server key" ext:cfg OR ext:log OR ext:txt
```

```
intitle:"(SSI Web Shell)" AND intext:"(ls -al)"
```

```
intitle:"index of" "admin/xml"
```

```
intitle:("Mini Shell") AND intext:("Upload File")
```

```
intitle:("Index of") AND intext:("c99.txt" OR "c100.txt")
```

```
inurl:/servicedesk/customer/user/login
```

```
inurl:"customer.aspx"
```

```
inurl:"index.php?db="
```

```
inurl:/phpmyadmin/index.php?db=
```

```
inurl:/phpMyAdmin/setup/index.php?phpMyAdmin=
```
