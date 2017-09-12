Test SNI DNS lookup using openssl
------------------------
```
## Use Burp Collaborator client to generate DNS name (On the menu - BURP/Burp Collaborator Client/Copy to Clipboard)
openssl s_client -connect xxx.yourdomain.xx:443 -servername zzzzzzzzzzzzzzzzzzzzzzzzzzzz.burpcollaborator.net
```


Check for HeartBleed
------------------------
```
# Look for 'heartbeat' in response
openssl s_client -connect xxx.yourdomain.xx:443 -tlsextdebug -msg
```
