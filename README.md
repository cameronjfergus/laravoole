#Laravoole

Laravel on Swoole

10x faster than php-fpm

##Depends On

<table>
	<tr>
		<td>php</td><td>>=5.5.9</td>
	</tr>
	<tr>
		<td>laravel/framework</td><td>5.1.*</td>
	</tr>
	<tr>
		<td>ext-swoole</td><td>>=1.7.19</td>
	</tr>
</table>


##Install
---------

```shell
 composer require acabin/laravoole
```

##Usage
-------

```shell
 vendor/bin/laravoole start | stop | reload | restart | quit
```

##Config
--------

In .env , use LARAVOOLE_* to config Laravoole.

###FastCGI or HTTP
------------------

```INI
 LARAVOOLE_MODE=Http
 LARAVOOLE_MODE=FastCGI
```

Default is set to Http, and you can also use FastCGI.


###pid_file
-----------

```INI
 LARAVOOLE_PID_FILE=/path/to/laravoole.pid
```

###deal\_with\_public
---------------------

Use this ***ONLY*** when developing

```INI
 LARAVOOLE_DEAL_WITH_PUBLIC=true
```

###Swoole
---------

Example:

```INI
 LARAVOOLE_HOST=0.0.0.0
```

Default host is 127.0.0.1:9050

See Swoole's document:

[简体中文](http://wiki.swoole.com/wiki/page/274.html)

[English](https://cdn.rawgit.com/tchiotludo/swoole-ide-helper/dd73ce0dd949870daebbf3e8fee64361858422a1/docs/classes/swoole_server.html#method_set)

##Work with nginx
-----------------

```Nginx
server {
	listen       80;
	server_name  localhost;

	root /path/to/laravel/public;

	location ~ \.(png|jpeg|jpg|gif|css|js)$ {
		break;
	}

	# proxy
	location / {
		proxy_set_header   Host $host:$server_port;
		proxy_set_header   X-Real-IP $remote_addr;
		proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_http_version 1.1;

		proxy_pass http://127.0.0.1:9050;
	}

	# fastcgi
	location / {
		include fastcgi_params;
		fastcgi_pass 127.0.0.1:9050;
	}
}
```

#License
[MIT](LICENSE)
