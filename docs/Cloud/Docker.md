# Docker 国内安装解决方案

- 支持Linux、Win、Mac
- https://github.com/tech-shrimp/docker_installer/releases

## Windows

- 任务栏搜索功能，启用"适用于Linux的Windows子系统" + "虚拟机平台"
- 管理员权限打开命令提示符，安装wsl2
wsl --set-default-version 2
wsl --update --web-download
- 下载Windows版本安装包，进入此项目的Release
https://github.com/tech-shrimp/docker_installer/releases

## Linux 

```
# 一键安装命令（每天自动从官网定时同步）
sudo curl -fsSL https://github.com/tech-shrimp/docker_installer/releases/download/latest/linux.sh| bash -s docker --mirror Aliyun

# 备用（如果Github访问不了，可以使用Gitee的链接）
sudo curl -fsSL https://gitee.com/tech-shrimp/docker_installer/releases/download/latest/linux.sh| bash -s docker --mirror Aliyun

# 启动docker
sudo service docker start
```
