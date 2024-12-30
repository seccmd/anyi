# FireWall

### ufw 
```
1. sudo apt-get install ufw

### Set the default access rules:
1. sudo ufw default deny incoming
2. sudo ufw default allow outgoing

### Set the service rules (SSH / HTTPS)
1. sudo ufw allow 22/tcp
2. sudo ufw allow 443/tcp

### Enable the firewall:
1. sudo ufw enable
2. sudo ufw disable
3. sudo ufw status

### If you ever add or delete rules you should reload the firewall
1. sudo ufw reload

注意
UFW是为了简化Iptables产生的，它在Iptables有自己的规则链。
Docker在启动时在Iptables会创建自己的规则链，所以不生效。

可以把规则添加到Docker连中即可。
iptables -I DOCKER -p all -j DROP

最后记得执行 iptables-save 保存规则
```

### ufw demo

```
netstat -antp | grep LISTEN | grep -v 127 | grep -v nginx
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      546/sshd: /usr/sbin
tcp        0      0 0.0.0.0:35707           0.0.0.0:*               LISTEN      275644/java
tcp        0      0 172.31.225.91:41371     0.0.0.0:*               LISTEN      275644/java

### Set the default access rules:
sudo ufw default deny incoming
sudo ufw default allow outgoing

### Set the service rules (SSH / HTTPS)
sudo ufw allow 22/tcp
sudo ufw allow 443/tcp
sudo ufw allow 8443/tcp
sudo ufw allow 9443/tcp

### Enable the firewall:
sudo ufw enable
```


### Linux的策略路由
- https://www.ujslxw.com/2020/10/19/44.html
