## Metasploit

Metasploit框架（Metasploit Framework,MSF）是一个开源工具，旨在方便渗透测试，它是由Ruby程序语言编写的模板化框架，具有很好的扩展性，便于渗透测试人员开发、使用定制的工具模板。 

#### 一、msf模块介绍
##### Auxiliaries（辅助模块）
    该模块不会直接在测试者和目标主机之间建立访问，它们只负责执行扫描、嗅探、指纹识别等相关功能以辅助渗透测试。

##### Exploit（漏洞利用模块）
    漏洞利用是指由渗透测试者利用一个系统、应用或者服务中的安全漏洞进行的攻击行为。流行的渗透攻击技术包括缓冲区溢出、Web应用程序攻击，以及利用配置错误等，其中包含攻击者或测试人员针对系统中的漏洞而设计的各种POC验证程序，用于破坏系统安全性的攻击代码，每个漏洞都有相应的攻击代码。

#####  Payload（攻击载荷模块）
    攻击载荷是我们期望目标系统在被渗透攻击之后完成实际攻击功能的代码，成功渗透目标后，用于在目标系统上运行任意命令或者执行特定代码，在Metasploit框架中可以自由地选择、传送和植入。攻击载荷也可能是简单地在目标操作系统上执行一些命令，如添加用户账号等。

##### Post（后期渗透模块）
    该模块主要用于在取得目标系统远程控制权后，进行一系列的后渗透攻击动作，如获取敏感信息、实施跳板攻击等。

##### Encoders（编码工具模块）
    该模块在渗透测试中负责免杀，以防止被杀毒软件、防火墙、IDS及类似的安全软件检测出来。

#### 二、msf主目录
	kali	/usr/share/metasploit-framework
	mac		/opt/metasplit-framework/embedded/framework/modules

#### 三、数据库管理
	msfdb init          	#初始化数据库，自动生成连接数据库配置文件
    /usr/share/metasploit-framework/config/database.yml
    msfdb reinit        	#重新初始化数据库
    msfdb delete        	#删除初始化数据库
    msfdb start         	#启动数据库
    msfdb stop          	#停止数据库
    apt-get install metasploit-framework           	#更新漏洞库

#### 四、msfconsole命令介绍
	db_status           	#查看数据库连接信息
    db_connect          	#连接数据库
    db_disconnect       	#断开数据库连接
    db_rebuild_cache    	#建立数据库缓存
    workspace          		#查看工作台
	workspace -a test  		#创建工作台
	workspace test     		#进入工作台
	workspace -d test  		#删除工作台
	db_nmap            		#nmap扫描   
	hosts              		#查看扫的主机
	hosts 192.168.1.1  		#查看指定的IP
	hosts -u           		#查看存活的主机
	hosts -S linux     		#搜索扫描结果
	hosts -c address,mac -S windows
	services -S 445    		#搜索包含445的主机    
	services -p 445
	services -c port,state  
	banner             		#显示启动banner信息
	connect            		#nc功能
	show               		#查看详细信息
	search             		#搜索 name:mysql 
	use exploit/windows/smb/ms08_067_netapi
	info               		#查看模块详细信息
	show options/payloads/targets/advanced/missing
	edit               		#编辑模块内容
	chek               		#验证漏洞是否存在
	creds              		#查看已暴力破解的信息
	loot               		#查看已获取的hash值
	vulns              		#查看扫描出来的漏洞
	db_export -f xml /root/msfbak.xml    #备份数据库
	db_import /root/msfbak.xml           #导入
	db_import /root/nmap.xml
	set rport          		#设置参数
	unset              		#取消设置
	setg rhosts 1.1.1.1		#设置全局
	save               		#保存配置
	   
	load openvas       		#调用外部插件
	openvas_connect    		#连接到外部插件
	unload openvas     		#卸载加载的插件
	loadpath           		#加载路径
	irb                		#开发接口
	resource r.rc      		#加载配置脚本
	msfconsole -r r.rc 











