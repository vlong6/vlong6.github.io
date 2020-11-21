## 04-wireshare&tcpdump

#### 一、wireshark
	抓包嗅探协议分析
	抓包引擎
    	Libpcap9——Linux
    	Winpcap10——Windows
	解码能力
	使用方法
    	选取抓包
    	混杂模式
    	实时抓包
    	保存和分析捕获文件
	常见协议包
    	数据包的分层结构
    	ARP\ICMP\TCP-三次握手\UDP\DNS\HTTP\FTP
	
	企业抓包部署方案
        sniffer
        cace\riverbed

#### 二、tcpdump
    	-i                #指定网卡
    	-s 0              #抓取完整数据包（默认只抓取68个字节 ）
    	-c 100            #抓去100个数据包
    	dst port ! 22     #不抓取目标端口22的数据包
    	src net 192.168.1.0/24    #源网络地址为192.168.1.0/24
    	-w a.cap          #保存数据包
	抓包
    	tcpdump -i eth0 -s 0 -w a.cap
    	tcpdump -i eth0 port 22 
	读取数据包
    	tcpdump -r a.cap
    	tcpdump -r -A file.pacp
    	tcpdump -x -r file.pacp
	显示筛选器
    	tcpdump -n -r http.cap | awk '{print $3}' | sort -u
    	tcpdump -n src host 1.1.1.1 -r http.cap
    	tcpdump -n dst host 1.1.1.1 -r http.cap
    	tcpdump -n tcp port 53 -r http.cap
    	tcpdump -A -n 'tcp[13]=24' -r http.cap
