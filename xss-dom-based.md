Testing for DOM based XSS
------------------------------
```
Modern browsers are not vulnerable?. Must use Internet Explorer for proof of concept
Open Internet Explorer
Press F12
Select the "Emulation" tab
Select "Document Mode" "7" (Try other versions if one does not work)
Reload the page

The "#" symbol in this case means pass everything after it to the DOM
http://xxx.xxx.xxx.xxx/xss/example9.php#<script>alert(123)</script>
```
