## Deploying Laravel App With Nginx in Windows System
### Nginx Configuration
```sh

worker_processes  1;

events {
	worker_connections	1024;
}

http {

	include		  mime.types;
	default_type  application/octet-stream;

	sendfile		on;

	keepalive_timeout  65;
	
	server {
		listen		 80;
		server_name	 localhost;
		root   C:\Web\Nginx\html\appmylara\public;
		
		add_header X-Frame-Options "SAMEORIGIN";
		add_header X-Content-Type-Options "nosniff";
		
		index index.php;
		charset utf-8;
		
		location / {
			try_files $uri $uri/ /index.php?$query_string;
		}
		
		location = /favicon.ico { access_log off; log_not_found off; }
		location = /robots.txt	{ access_log off; log_not_found off; }
		
		error_page 404 /index.php;
		
		location ~ \.php$ {
			fastcgi_pass   127.0.0.1:9123;
			fastcgi_param  SCRIPT_FILENAME	$realpath_root$fastcgi_script_name;
			include		   fastcgi_params;
		}
		
		location ~ /\.(?!well-known).* {
			deny all;
		}
	}
}

```
## NPM Install
```sh
npm install
npm run build
npm run dev
```
### Windows Host File Configuration
* C:\Windows\System32\drivers\etc\hosts
```sh
127.0.0.1 localhost
```
### PHP CGI
* Hidden Console App
```sh
@ECHO OFF
ECHO Starting PHP FastCGI...
set PATH=C:\Programs\Sdk\Php;%PATH%
C:\Web\Nginx\hcon\hcon.exe C:\Programs\Sdk\Php\php-cgi.exe -b 127.0.0.1:9123
```
### Nginx Start Stop
```sh
start nginx
nginx -s stop
```

* [Ref](https://learn.microsoft.com/en-us/troubleshoot/developer/webapps/aspnetcore/practice-troubleshoot-linux/2-7-configure-second-nginx-site-hostname)
