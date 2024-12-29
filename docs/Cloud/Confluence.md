### 准备VPS 2C4G

### 安装Java

`$ apt install openjdk-8-jre-headless`

### 安装PSQL

```
$ apt install postgresql
$ su - postgres
$ psql
  create user jira with password 'jirapassword';
  create database jira owner jira;
  grant all on database jira to jira;
$ psql -U username databasename < /data/dum.sql 
```

### 安装Jira

下载地址: https://www.atlassian.com/software/jira/update

```
$ ./atlassian-jira-software-8.20.8-x64.bin
  Installation Directory: /opt/atlassian/jira 
  Home Directory: /var/atlassian/application-data/jira 
  HTTP Port: 8080 
  RMI Port: 8005 
```

### 补丁

```
  地址: https://gitee.com/pengzhile/atlassian-agent/attach_files/832833/download/atlassian-agent-v1.3.1.zip
  目录: /opt/atlassian/atlassian-agent

  # 启动运行补丁: vi /etc/init.d/confluence
  # Padding hhll
  export JAVA_OPTS="-javaagent:/opt/atlassian/atlassian-agent/atlassian-agent.jar ${JAVA_OPTS}"
  /etc/init.d/jira start

  # 获取激活码 KeyGen
  Enter your Confluence license key
  java -jar /opt/atlassian/atlassian-agent/atlassian-agent.jar
  java -jar /opt/atlassian/atlassian-agent/atlassian-agent.jar -p jira -m admin@admin.com -n my_name -o admin -s XXXX-XXXX-XXXX-XXXX
```

### 启动服务:

`/etc/init.d/confluence start`

### 初始化步骤

- 设置数据库、设置管理员
- http://x.x.x.x:8080
