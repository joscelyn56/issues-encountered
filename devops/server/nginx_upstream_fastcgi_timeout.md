# Nginx Upstream FastCGI Timeout

FastCGI is an upstream server used to proxy php applications on nginx.

## Problem

This error occurs during high traffic seasons where the server is slow to respond to request and further comes in,
it causes the server to block other requests coming within the same period.

```bash
2021/06/10 22:03:24 [error] 255#255: *1111 upstream timed out (110: Connection timed out) while reading response header from upstream, client: 10.244.1.57, server: _, request: "GET /api/user/profile HTTP/1.1", upstream: "fastcgi://127.0.0.1:9000", host: {host}, referrer: {request source}
```

## Fix

The issue can be fixed by one or the combination of the methods below

### Adjustment in timeout settings
Usually, adjusting the timeout settings is one of the methods to fix 504 error.
Edit the file /etc/nginx/conf.d/timeout.conf and added the following parameters to file “timeout.conf”.
```bash
proxy_connect_timeout       600;
proxy_send_timeout          600;
proxy_read_timeout          600;
send_timeout                600;
```

### Finally, we restarted the service.
```bash
service nginx restart
```

### Modifying Other Nginx settings

Sometimes, increasing values in “timeout.conf” doesn’t resolve this issue. Then, our Support Engineers add codes in “nginx.conf”. In addition, if the values are already preset in “nginx.conf”, we will increase the value.

Then, we add the following snippet to “timeout.conf”.

```bash
client_header_timeout 3000;
client_body_timeout 3000;
fastcgi_read_timeout 3000;
client_max_body_size 32m;
fastcgi_buffers 8 128k;
fastcgi_buffer_size 128k;
```

### Finally, we restart the service.
```bash
service php-fpm restart
service nginx restart
```

### Modification in PHP settings
locate the “/etc/php.ini” file and increase the value “max_execution_time” by adding the following entry.
```bash
max_execution_time = 150
```
Additionally, we raised the value of request_terminate_timeout setting in php.ini file too.
```bash
request_terminate_timeout = 150
```

### Nginx virtual host configuration settings

Similarly, fix may involve modifying Nginx virtual host configuration too. Here, to fix the php file access, 
in Nginx virtual host configuration, add FastCGI read timeout variable.
```bash
location ~* \.php${
    include fastcgi_params;
    fastcgi_index index.php;
    fastcgi_read_timeout 150;
    fastcgi_pass 127.0.0.1:9000;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
}
```

Then, we restart PHP-FPM and Nginx.
```bash
service php-fpm restart
service nginx restart
```

## Source
[https://bobcares.com/blog/504-timeout-nginx/](https://bobcares.com/blog/504-timeout-nginx/)

Further explanation on nginx timeout

[https://developpaper.com/detailed-explanation-of-nginx-timeout-configuration/](https://developpaper.com/detailed-explanation-of-nginx-timeout-configuration/)
