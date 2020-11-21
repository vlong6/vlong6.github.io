## 03-Linux常用命令

#### 一、查看系统信息命令

	whoami                    #显示当前登录用户
	id                        #显示当前用户和组
	last                      #显示最后一个登录的用户
	df -h                     #显示磁盘使用情况
	echo "root:pass" | chpasswd		#重置密码
	strings /usr/local/bin/blah		#查看二进制文件
	uname -a                  #查看内核版本
	cat /proc/version
	rpm -q kernel
	dmesg | grep Linux
	PATH=$PATH:/new-paht      #添加环境变量
    cat /etc/profile          #环境变量信息 
    cat /etc/baserc
    cat ~/.bash_profile
    cat ~/.bashrc
    env/set                   #设置环境变量
    history                   #查看历史命令
    cat /etc/issue            #查看linux发型版本
    cat /etc/*-release
    cat /etc/debian_version   #显示Debian版本号
    cat /etc/*-release        #显示Ubuntu版本号
    dpkg -l                   #显示几个Debian的Linux发行版本的所有安装的包
    rpm -qa                   #列出已安装的RPM包
	gparted                   #分区编辑器，删除磁盘分区
	parted                    #磁盘分区  

#### 二、yum常用命令

	yum update                #更新所有rpm包
    yum update httpd          #更新软件包
    yum install httpd         #安装软件
    yum --exculed=package kernul* update    #排除软件包更新
    yum remove httpd          #删除软件包
    yum list httpd            #列出yum包相关的信息
    yum provides httpd        #显示软件包的用途
    yum info httpd            #显示软件包的详细信息
    yum list                  #列出已安装的数据包
    yum grouplist             #列出yum包组
    yum groupinstall 'Development Tools'        #安装yum包组

#### 三、网站搭建

    iptables -F
    yum -y install httpd php php-mysql mysql mysql-server
    service httpd start
    service mysqld start
    mysqladmin -uroot password 123
    mysql -uroot -p





