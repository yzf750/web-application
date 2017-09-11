Mirror website with wget
------------------------
```
wget -mkEpnp http://www.yoursite.org
```
Curl - Test web connections from console and view returned results
------------------------
```
curl -kis  http://xxx.xxx.xxx.xxx/etc/passwd
```
Curl - Grab HTTP Headers
------------------------
HTTP
```
curl -LIN http://www.yoursite.com
```
HTTPS
```
curl -LIN -k https://www.yoursite.com
```
Find Writeable Directories (Good for uploading shells)
------------------------
```bash
find / -type d \( -perm -g+w -or -perm -o+w \) -exec ls -adl {} \;
```
```bash
find / -type d \( -perm -g+w -or -perm -o+w \) -exec ls -adl {} \; | grep www-data
```

Mass download files by id
------------------------
```bash
#!/bin/bash
   for i in `seq 1000 5000`;
      do
         wget https://your.site.com:80/pathtodownloads/file.php?id=$i
      done
```
Nikto scan all and output to html
------------------------
```
nikto -Display V -o results.html -Format htm -h http://xxx.xxx.xxx.xx:80/directory/
```

Test SNI DNS lookup using openssl
------------------------
```
## Use Burp Collaborator client to generate DNS name (On the menu - BURP/Burp Collaborator Client/Copy to Clipboard)
openssl s_client -connect xxx.yourdomain.xx:443 -servername zzzzzzzzzzzzzzzzzzzzzzzzzzzz.burpcollaborator.net
```

