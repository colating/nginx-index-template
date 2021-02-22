# Nginx Index Template

Good!
Thank Franc.

The orignal :  https://github.com/jbox-web/nginx-index-template

----------------- 

Bootstrap version of : [dirlist.xslt](https://gist.github.com/wilhelmy/5a59b8eea26974a468c9) with breadcrumb

To use it :

```nginx
server {
  server_name   foo.bar.baz;
  listen        80;
  root          /home/aptly/endpoints;

  autoindex     on;
  autoindex_format xml;

  access_log    /var/log/nginx/aptly.access.log;
  error_log     /var/log/nginx/aptly.error.log;


  location / {
    try_files $uri @autoindex;
  }

  location @autoindex {
    xslt_stylesheet /home/aptly/nginx_template.xslt path='$uri';
  }
}

```

![Screenshot](/images/screenshot.png?raw=true "Screenshot")


===================== 

	Perhas need to change as follow:
	1. To compatible the pc and the mobile phone, add follow:
  	   <xsl:template match="/">
	     <html>
	       <head>
		 <title>Colating Documents</title>
		 <meta charset="utf-8" />
		 <meta http-equiv="content-type" content="text/html" />  ## Colating add
		 <meta http-equiv="X-UA-Compatible" content="IE=edge" />  ## Colating add
		 <meta name="viewport" content="width=device-width, initial-scale=1.0" />  ## Colating add

	2. Font size:
				font-weight: 620;  ## Colating add
				font-size: 120%;  ## Colating add
				line-height: 100%"  ## Colating add
			  }
			</style>
		  </head>

	3. setup: only index the "docs" dir.
	----------- 
	## Colating Change:
	location / {
	  try_files $uri $uri/ =404;    ## Colating add
	  ## try_files $uri @autoindex;  ## Colating cancel:
	}
	----------- 
	## Colating Change:
	location ~ ^/docs(/.*){
	      autoindex on;
	      autoindex_format xml;
	      xslt_stylesheet /home/aptly/nginx_template.xslt path='$uri';
	 }



