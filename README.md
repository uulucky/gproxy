# 参考网站
https://google.uulucky.com
# gproxy
三行代码实现谷歌反代 nginx 里新建 server
```
server {
        listen              443 ssl;
        server_name         google.uulucky.com;
        ssl on;
        ssl_certificate   encrypt/google.uulucky.com.pem;
        ssl_certificate_key  encrypt/google.uulucky.com.key;
        ssl_session_timeout 5m;
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;

        access_log  logs/google.access.log;

        location / {
            proxy_pass https://www.google.com.hk;
            proxy_redirect ~^https://www.google.com.hk(.*)   https://google.uulucky.com$1;
            proxy_redirect ~^https://www.google.com(.*)   https://google.uulucky.com$1;
        }
    }
```
## License
WTFPL
