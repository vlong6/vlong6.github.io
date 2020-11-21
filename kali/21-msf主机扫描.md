## Metasploit 主机扫描

扫描和收集信息是渗透测试中的第一步，其主要目标是尽可能多地发现有关目标机器的信息。获取的信息越多，渗透的概率就越大。该步骤的主要关注点是目标机器IP地址、可用服务、开放端口等。

#### 一、使用辅助模块进行端口扫描
	msf6 > search portscan
	Matching Modules
	================
	   #  Name                                              Disclosure Date  Rank    	Check  Description
	   -  ----                                              ---------------  ----    	-----  -----------
	   0  auxiliary/scanner/http/wordpress_pingback_access                   normal  	No     Wordpress Pingback Locator
	   1  auxiliary/scanner/natpmp/natpmp_portscan                           normal  	No     NAT-PMP External Port Scanner
	   2  auxiliary/scanner/portscan/ack                                     normal  	No     TCP ACK Firewall Scanner
	   3  auxiliary/scanner/portscan/ftpbounce                               normal  	No     FTP Bounce Port Scanner
	   4  auxiliary/scanner/portscan/syn                                     normal  	No     TCP SYN Port Scanner
	   5  auxiliary/scanner/portscan/tcp                                     normal  	No     TCP Port Scanner
	   6  auxiliary/scanner/portscan/xmas                                    normal  	No     TCP "XMas" Port Scanner
	   7  auxiliary/scanner/sap/sap_router_portscanner                       normal  	No     SAPRouter Port Scanner

#### 一、使用辅助模块进行服务扫描
	msf6 > search scanner
	Matching Modules
	================
	   #    Name                                                                     Disclosure Date  Rank    Check  Description
	   -    ----                                                                     ---------------  ----    -----  -----------
	   0    auxiliary/admin/appletv/appletv_display_image                                             normal  No     Apple TV Image Remote Control
	   1    auxiliary/admin/appletv/appletv_display_video                                             normal  No     Apple TV Video Remote Control
	   2    auxiliary/admin/smb/check_dir_file                                                        normal  No     SMB Scanner Check File/Directory Utility
	   3    auxiliary/admin/teradata/teradata_odbc_sql                               2018-03-29       normal  No     Teradata ODBC SQL Query Module
	   4    auxiliary/bnat/bnat_scan                                                                  normal  No     BNAT Scanner
	   5    auxiliary/gather/citrix_published_applications                                            normal  No     Citrix MetaFrame ICA Published Applications Scanner
	   6    auxiliary/gather/enum_dns                                                                 normal  No     DNS Record Scanner and Enumerator
	   7    auxiliary/gather/hp_enum_perfd                                                            normal  No     HP Operations Manager Perfd Environment Scanner
	   8    auxiliary/gather/natpmp_external_address                                                  normal  No     NAT-PMP External Address Scanner
	   9    auxiliary/gather/windows_deployment_services_shares                                       normal  No     Microsoft Windows Deployment Services Unattend Gatherer	
	   .....

#### 一、使用Nmap扫描
	msf6 > 
	msf6 > nmap
	[*] exec: nmap
	Nmap 7.80 ( https://nmap.org )
	Usage: nmap [Scan Type(s)] [Options] {target specification}
	TARGET SPECIFICATION:
	  Can pass hostnames, IP addresses, networks, etc.
	  Ex: scanme.nmap.org, microsoft.com/24, 192.168.0.1; 10.0.0-255.1-254
	  -iL <inputfilename>: Input from list of hosts/networks
	  -iR <num hosts>: Choose random targets
	  --exclude <host1[,host2][,host3],...>: Exclude hosts/networks
	  --excludefile <exclude_file>: Exclude list from file
	HOST DISCOVERY:
	  -sL: List Scan - simply list targets to scan
	  -sn: Ping Scan - disable port scan
	  -Pn: Treat all hosts as online -- skip host discovery
	  -PS/PA/PU/PY[portlist]: TCP SYN/ACK, UDP or SCTP discovery to given ports
	  -PE/PP/PM: ICMP echo, timestamp, and netmask request discovery probes
	  -PO[protocol list]: IP Protocol Ping
	  -n/-R: Never do DNS resolution/Always resolve [default: sometimes]
	  --dns-servers <serv1[,serv2],...>: Specif

