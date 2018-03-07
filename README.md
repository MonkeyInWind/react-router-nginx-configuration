# 项目用了react-router 并且前端和服务端在同一项目nginx的配置

react项目用了react-router放到服务器上开了node服务 配置nginx  
>  server {  
  	server_name xxx.xxxxxxx.com;  
  	location / {  
  		proxy_pass http://11.11.11.11:1111/; (node服务端口)  
  		root html;  
  		index index.html index.htm;  
  	}  
  }  

打开网站发现只能从主页访问 进到子页面之后刷新会 not found 这是因为他会根据url去找路径下的html  但是react项目只有一个
index.html作为入口文件  所以这种配置不合适 需要把html文件改成绝对路径  并且无论uri是否变化  都返回index.html  
>server {  
	server_name xxx.xxxxxx.com;  
	location / {  
		root /xxx/xxx/xxx/www/build;  
		try_files $uri /index.html;  
	}  
	location ^~ /api/ {  
		proxy_pass http://11.11.11.11:1111/;(服务端接口做代理)  
	}  
}  

