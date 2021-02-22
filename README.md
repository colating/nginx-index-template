# Nginx Index Template

The orignal :https://github.com/jbox-web/nginx-index-template

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

	Have Change:
	1. To compatible the pc and the mobile phone, add follow:
			<meta http-equiv="content-type" content="text/html" />
			<meta http-equiv="X-UA-Compatible" content="IE=edge" />
			<meta name="viewport" content="width=device-width, initial-scale=1.0" />

	2. Font size:	/* Colating change ----------- */
				font-weight: 620;
				font-size: 120%;
				line-height: 100%"
			  }
			</style>
		  </head>

	3. setup: only index the "docs" dir.
	----------- 
	Change:
	location / {
	  try_files $uri $uri/ =404;
	  ## try_files $uri @autoindex;  ## cancel:
	}
	----------- 
	Need:
	location ~ ^/docs(/.*){
	      autoindex on;
	      autoindex_format xml;
	      xslt_stylesheet /home/aptly/nginx_template.xslt path='$uri';
	 }



