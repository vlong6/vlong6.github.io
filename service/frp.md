## frp

#### 一、下载地址
    
    https://github.com/fatedier/frp/releases

#### 二、帮助文档
    
    https://github.com/fatedier/frp/blob/master/README_zh.md
 
#### 三、frp内网端口映射
    
    服务器端 
        [common] 
        bind_port = 7000
        token = password
 
    客户端
        [common] 
        server_addr = 192.168.1.112 
        server_port = 7000 
        token = password
     
        [msf] 
        type = tcp 
        local_ip = 127.0.0.1 
        local_port = 80 
        remote_port = 80 

#### 四、frp配置socks5
    服务器端 
        [common]
        bind_port = 8080

    客户端
        [common]
        server_addr = xx.xx.xx.xx
        server_port = 8080
        #服务端口使用Web常见端口
        [socks5]
        type = tcp
        remote_port = 8088
        plugin = socks5
        use_encryption = true 
        use_compression = true
        #socks5口令
        #plugin_user = SuperMan
        #plugin_passwd = XpO2McWe6nj3
 
#### 五、报错处理
    
    [control.go:236] authorization timeout 

    修复为北京的时区CST 
        cp /etc/localtime /etc/localtime.bak 
        ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime 
    同步时间 
        date -s "YYYY-MM-DD HH-MM-SS" 
        hwclock -w 

