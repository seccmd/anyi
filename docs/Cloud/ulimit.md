# ulimit

  ulimit -a

### 系统设置

```
# cat /etc/security/limits.conf
root soft core unlimited
root hard core unlimited
root soft nproc 1000000
root hard nproc 1000000
root soft nofile 100000
root hard nofile 100000
root soft memlock 32000
root hard memlock 32000
root soft msgqueue 8192000
root hard msgqueue 8192000
soft core unlimited
hard core unlimited
soft nproc 1000000
hard nproc 1000000
soft nofile 100000
hard nofile 100000
soft memlock 32000
hard memlock 32000
soft msgqueue 8192000
hard msgqueue 8192000
```