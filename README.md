Open index.html in browser


Nginx server block example
```
location ~ /demonopush/? {
        root /var/http2demo/;
        index index.html;
        delay 200ms;
}

location ~ /demopush/? {
    location  ~* \.(png|js|css)$ {
        root   /var/http2demo/;
        index  index.html;
    }

    location  ~* / {
        root /var/http2demo/;
        index index.html;
        delay 200ms;

         if ($request_uri = /demopush/) {
            add_header link "</demopush/about.html>; rel=preload;";
            add_header link "</demopush/js/jquery2-2.2.3.min.js>; rel=preload;";
            add_header link "</demopush/js/bootstrap2.js>; rel=preload;";
            add_header link "</demopush/css/bootstrap2.css>; rel=preload;";
            add_header link "</demopush/images/placeholder.png>; rel=preload;";
            add_header link "</demopush/images/placeholder2.png>; rel=preload;";
            add_header link "</demopush/images/placeholder3.png>; rel=preload;";
            add_header link "</demopush/images/placeholder4.png>; rel=preload;";
         }
    }
}
```
