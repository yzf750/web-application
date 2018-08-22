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
Curl - POST data to a url
------------------------
```
curl -k -i -d "zzzz=1111111&yyyy=2222&xxxxxx=123456" -X POST https://xxx.xxx.xxx.xxx/url/to/post/to.php
