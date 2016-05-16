Open index.html in browser


Nginx server block example
```
server {
  listen       443 http2 ssl;
  server_name  h2demo;
  tcp_nodelay     on;
  tcp_nopush      off;

  http2_server_push on;
  http2_max_push_per_stream     200;
  http2_max_push_per_connection 20000;

  location /demov2push/ {
    location ~* \.(png|js|css)$ {
      root   /var/h2demo/;
      index  index.html;
    }

    location ~* / {
      root /var/h2demo/;
      index index.html;

      if ($request_uri = /demov2push/index.html) {
        add_header link "</demov2push/js/jquery2-2.2.3.min.js>; rel=preload;";
        add_header link "</demov2push/js/bootstrap2.js>; rel=preload;";
        add_header link "</demov2push/css/bootstrap2.css>; rel=preload;";
        add_header link "</demov2push/images/placeholder2.png>; rel=preload;";
      }
    }
  }
}
```
