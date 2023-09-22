## Deploying Laravel App With Nginx in Windows System
### Nginx Configuration
```sh
server {
        listen       80;
        server_name  appmylara.com;
    	root   C:\Web\Nginx\html\appmylara\public;
    		
    	add_header X-Frame-Options "SAMEORIGIN";
    	add_header X-Content-Type-Options "nosniff";
    		
    	index index.php;
    	charset utf-8;
    		
        location /public {
            try_files $uri $uri/ /index.php?$query_string;
        }
    		
    	location = /favicon.ico { access_log off; log_not_found off; }
    	location = /robots.txt  { access_log off; log_not_found off; }
    		
    	error_page 404 /index.php;
    		
    	# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        location ~ \.php$ {
            fastcgi_pass   127.0.0.1:9123;
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
            #fastcgi_param  SCRIPT_FILENAME  $realpath_root$fastcgi_script_name;
            include        fastcgi_params;
        }
    		
    	location ~ /\.(?!well-known).* {
    		deny all;
    	}
		
    }
```

### Windows Host File Configuration
* C:\Windows\System32\drivers\etc\hosts
```sh
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost

127.0.0.1 localhost
127.0.0.1 appmylara.com
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
