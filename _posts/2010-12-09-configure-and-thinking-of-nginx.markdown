---
layout: post
title: nginx配置及反思
date: '2010-12-9'
comments: true
---
先把配置文件发上来吧，至于分析。。以后有时间了再做。。。今天太晚了。。
```
user nginx nginx; #运行用户及用户组
worker_processes 4; #进程数，等于CPU内核数或cpu内核数的两倍

error_log  /data/logs/nginx_error.log crit; #运行记录，只记录严重错误

worker_rlimit_nofile 65535; #文件最大打开数

events {
	use epoll; #使用epoll内核
	worker_connections 65535; #工作最大连接数
}

http {
	include mime.types;
	default_type  application/octet-stream;

	sendfile on;
	tcp_nopush on;

	client_header_timeout 30;
	client_body_timeout 30;
	send_timeout 30;

	keepalive_timeout  0;

	client_max_body_size 50m;
	fastcgi_connect_timeout 900;
	fastcgi_send_timeout 900;
	fastcgi_read_timeout 900;
	fastcgi_buffer_size 64k;
	fastcgi_buffers 4 64k;
	fastcgi_busy_buffers_size 128k;
	fastcgi_temp_file_write_size 128k;
	fastcgi_cache_valid 200 302 1h;
	fastcgi_cache_valid 301 1d;
	fastcgi_cache_valid any 1m;
	fastcgi_cache_min_uses 1;
	fastcgi_cache_use_stale error timeout invalid_header http_500;

	open_file_cache max=204800 inactive=20s;
	open_file_cache_min_uses 1;
	open_file_cache_valid 30s;
	tcp_nodelay on;
	gzip on;
	gzip_min_length 1k;
	gzip_buffers 4 16k;
	gzip_http_version 1.0;
	gzip_comp_level 2;
	gzip_types text/plain application/x-javascript text/css application/xml;
	gzip_vary on;

	limit_zone crawler $binary_remote_addr 10m; #配置限制


	server {
		listen 80;
		server_name rs.xidian.edu.cn,resource.xidian.edu.cn;
		root /data/webserver/bt/web;
		index index.php index.html;

		error_page 502 = /error/502.html;

		location /bbs {
			index index.php;
			alias /data/webserver/bt/bbs;
		}

		location ~ ^/bbs/(.+\.php)$ {
			alias /data/webserver/bt/bbs/$1;
			include fastcgi_params;
			fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
			fastcgi_pass 127.0.0.1:9000;
			fastcgi_index index.php;
		}

		location ^~ /announce.php {
			limit_conn crawler 10;
			proxy_pass http://resource.xidian.edu.cn;
		}

		location /status {
			stub_status on;
		}

		location ~ .*\.php5?$ {
			include fastcgi_params;
			root /data/webserver/bt/web;
			fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
			fastcgi_pass 127.0.0.1:9000;
			fastcgi_index index.php;
		}

		location ~* .(gif|jpg|jpeg|png|bmp|swf)$ {
			expires 30d;
		}
		location ~ .*\.(js|css)?$ {
			expires 1h;
		}

	}
}
```