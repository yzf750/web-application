Use Kerberos Authentication
------------------------
```
#Download Link
https://github.com/portswigger/kerberos-authentication
#Install from within Burp
"Kerberos Authentication"

To configure

"Domain DNS Name" 
- enter fqdn for Windows domain - eg. mywinddomain.secondlevel.tld
"KDC Host"
- Enter fqdn of domain controller - eg domaincontname.mywinddomain.secondlevel.tld

"Username"
- enter username (only the username and without the mywinddomain/username)
"Password"
- enter password

"krb5.conf file"
- may need to create one, run tests for each of the settings above to determin
```
