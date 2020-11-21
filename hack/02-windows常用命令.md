## 02-windows常用命令

#### 一、windows敏感文件
	c:\Windows\System32\config\sam          #密码文件
	c:\Windows\System32\drivers\etc\hosts   #本地dns文件
	c:\boot.ini                             #查看系统版本
	c:\windows\system32\inetsrv\metabase.xml    #iis配置文件
	c:\windows\repair\sam                   #系统初次密码
	c:\program files\mysql\my.ini           #mysql配置
	c:\program files\mysql\data\mysql\user.myd #mysql root
	c:\windows\php.ini
	c:\windows\my.ini

#### 二、cmd命令
##### 1、文件类操作
	color                   #修改背景颜色
	type 123.txt            #查看文本
	tree                    #显示目录树
	dir                     #查看当前目录内容
	cd                      #切换目录
	md                      #创建目录
	rd                      #删除目录
	del                     #删除文件
	ren                     #重命名
	copy                    #复制文件
	move                    #移动文件
	attrib 文件名           #查看文件属性
	attrib 文件名 -A -R -S -H 或 +A +R +S +H    #去掉或添加某文件的属性，存档、只读、系统、隐藏
	copy con 123.txt        #创建文件
	    hello
	    Ctrl + Z    Enter


##### 2、网络信息获取
	arp -a                  #查看局域网中的MAC地址
	getmac                  #查看本机的MAC地址
	net view                #查看局域网中的主机
	ipconfig                #查看ip地址
	ipconfig /all           #查看网络所有信息
	ipconfig /release       #释放ip地址
	ipconfig /renew         #重新获取ip地址
	ipconfig /flushdns      #清楚本地DNS缓存
	ipconfig /displaydns    #显示本地DNS内容
	ipconfig /regiesterdns  #DNS客户端项服务器进行注册

##### 3、用户类操作
	query user                          #查看最近登录
	net user testuser 123 /add          #创建用户
	net user testuser 456               #修改密码
	net user testuser /del              #删除用户
	net user testuser /active:yes       #启用账户
	net user testuser /active:no        #禁用账户
	net user                            #查看用户
	net user testuser                   #查看用户属性
	net localgroup testuser /add        #创建组
	net localgroup testuser /del        #删除组
	net localgroup                      #查看组
	net localgroup administrators testuser /add     #添加用户到组
	net localgroup administrators testuser /del     #把用户从组中删除

##### 4、系统命令
	explorer.exe            #桌面进程
	start baidu.com         #打开百度
	start 123.txt           #打开文本
	systeminfo              #获取系统详细信息
	shutdown -r -s -a -t 180 -c "描述"  #重启、关机、取消、设置时间、描述
	msg administrator "hello backer"    #发送消息
	conver e:/fs:ntfs                   #fat32转换成ntfs
	format e:/fs:nfs                    #磁盘格式化
	net share                           #查看本地共享
	net share ipc$                      #开启ipc$共享
	net share ipc$ /del                 #删除共享
	net share abcd=d:\abcd              #共享文件
	net use k: \\192.168.1.1\c$         #远程挂载到本地
	net use k: /del                     #删除
	tasklist                            #进程
	taskkill 进程id
	taskkill /im cmd.exe                #结束进程
	nbtstat -n                          #查看本地计算机netBIOS名
	nbtstat -a ip/hostname              #查看指定计算机NetBIOS名
	netstat -an                         #查看开放的端口
	netstat -n                          #查看端口的网络连接情况
	netstat -v                          #查看正在进行的工作
	netsta -ano |findstr "3388"         #查找端口
	net start                           #查看开启了哪些服务
	net start 服务名                     #开启服务
	net sotp 服务名                      #停止服务
	net stop mpssvc                     #打开防火墙
	netsh firewall set opmode mode=enable（公网防火墙）
	at id号                             #开启已注册计划
	at /delete                          #停止所有计划
	at                                  #查看所有计划任务
	inetcpl.cpl                         #Internet属性
	bcdedit.exe -set loadoptions DDISABLE_INETGRITY_CHECKS  #禁用数字签名
	get-hostfix -id KB3045999           #卸载补丁

