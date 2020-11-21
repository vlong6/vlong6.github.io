## Centos搭建ss

#### 一、下载
	wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh
 
#### 二、安装
	chmod +x shadowsocksR.sh
	./shadowsocksR.sh 2>&1 | tee shadowsocksR.log

#### 三、启动
	/etc/init.d/shadowsocks-r start | stop | restart | status

#### 四、卸载
	./shadowsocksR.sh uninstall