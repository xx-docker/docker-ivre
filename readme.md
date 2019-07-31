# 安装指南
- [官方指南](https://doc.ivre.rocks/en/latest/usage/web-ui.html#)
- [安装教程](https://www.open-open.com/lib/view/open1452067486636.html)
- mkdir -m 1777 var_lib_mongodb var_log_mongodb ivre-share
- docker-compose up -d 

## Vagrant-centos7 安装指南
- rpm -ivh https://releases.hashicorp.com/vagrant/2.2.5/vagrant_2.2.5_x86_64.rpm
- vagrant up  --no-parallel

## 容器清理
- docker ps -a | grep ivre | awk '{print $1}' | xargs docker stop | xargs docker rm