# SSL-TLS-Cert

### Let's Encrypt

说明：Let's Encrypt —— 是一个由非营利性组织 互联网安全研究小组（ISRG）提供的免费、自动化和开放的证书颁发机构（CA），简单的说，就是为网站提供免费的 SSL/TLS 证书。acme.sh 实现了 acme 协议,可以从letsencrypt生成免费的证书。接下来将为大家介绍怎样申请Let's Encrypt通配符证书。

- 使用acme.sh申请Let's Encrypt免费的SSL证书
- https://cloud.tencent.com/developer/article/1877928
- 详解 ACME V2 (RFC 8555) 协议，你是如何从Let's Encrypt 申请到证书的 
- https://zhuanlan.zhihu.com/p/75032510

```
# 使用 Let's Encrypt 获取 SSL 证书的第一步是在服务器上安装 Certbot
sudo apt-get update
sudo apt install certbot python3-certbot-nginx

# 为域名获取证书

sudo certbot --nginx --nginx-server-root /usr/local/nginx/conf/  -d seccmd.net -d www.seccmd.net

sudo certbot --expand --nginx --nginx-server-root /usr/local/nginx/conf/  -d seccmd.net -d www.seccmd.net -d 123.seccmd.net -d sec123.seccmd.net

# 由于Let's Encrypt的证书有效期只有90天，到期后使用certbot renew命令来更新证书，我们只需要把该命令做成任务定期执行即可
sudo systemctl status certbot.timer

# 最后测试任务运行情况
sudo certbot --nginx --nginx-server-root /usr/local/nginx/conf/ renew --dry-run

1.查看证书：
certbot certificates

2.删除某个安装了证书的域名：
certbot delete --cert-name example.com

3.重新创建和更新现有证书
certbot --expand -d existing.com,example.com,newdomain.com

使用教程：https://eff-certbot.readthedocs.io/en/stable/using.html
```

### SSL Self-Signed 自签名

```
1. Create and install a self-signed SSL certificate:
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/certificate.key -out /etc/nginx/certificate.crt
$ sudo chmod 400 /etc/nginx/certificate.key

2.Follow the prompts. 输入证书信息
Tip: It is IMPORTANT that the Common Name be set properly.  字段Common Name非常重要
Enter your fully qualified domain name(FQDN) here or, if you don’t have a FQDN,  输入域名
use your public IP address.  没有域名输入IP地址
For example, my FQDN for the chat server is chat.inumio.com .例如：chat.inumio.com

3. 配置 Nginx 删除默认SSL配置文件，拷贝下面配置
$ sudo nano /etc/nginx/sites-enable/default
# HTTPS Server
    server {
        listen 443 ssl;
        server_name _;

        error_log /var/log/nginx/rocketchat_error.log;

        ssl_certificate /etc/nginx/certificate.crt;
        ssl_certificate_key /etc/nginx/certificate.key;
        ssl_protocols TLSv1.2;
        ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';
        ssl_prefer_server_ciphers on;
        ssl_session_cache shared:SSL:20m;
        ssl_session_timeout 180m;

        location / {
            proxy_pass http://chat.inumio.com:3000/;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
            proxy_set_header Host $http_host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto https;
            proxy_set_header X-Nginx-Proxy true;
            proxy_redirect off;
        }
    }
```
