shorturl-nginx
----------

A URL Shortener with analytics based on Nginx and Redis


Setup
---------

 - Start a redis instance
 - Build your nginx with **lua-nginx-module** and **set-misc-nginx-module**
 - Copy the lua script conf/lua/n3r/**urlshortener_eval.lua** to your own nginx **conf/lua/n3r/** directory, and update the redis configurations in the **connect** function
 - Copy the html/**shorten-ui.html** to your own nginx **html** directory
 - Download [lua-resty-redis](https://github.com/agentzh/lua-resty-redis) and copy the lib/resty/**redis.lua** to your own nginx **conf/lua/resty/** directory
 - Add the follow configurations to your nginx.conf, then start your nginx

> **http block:** lua_package_path
>
> **server block:** location a)shorten-ui.html b)shorten c)^/0[0-9a-zA-Z]{1,12}$
>
> You could find these configurations in my **conf/nginx.conf** 

Basic Usage
---------

#### <i class="icon-file"></i> Create a short url
    http://localhost:8088/shorten?url=http://www.google.com
> **NOTE:** Do not forget the **http://** prefix within the **url** parameter

#### <i class="icon-folder-open"></i> Visit the short url
    Just visit the url that the previous step returned

#### <i class="icon-pencil"></i> Web UI
    http://localhost:8088/shorten-ui.html
> **NOTE:** In this page, you could input a URL, then get the shorten form

#### <i class="icon-file"></i> Create a random short url
    http://localhost:8088/shorten?url=http://www.google.com&random=true
    
#### <i class="icon-file"></i> Query source url by the short 
    http://localhost:8088/shorten-qrybyshort?url=http://t.cn/0asd
