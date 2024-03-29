# 安装指南
- [官方指南](https://doc.ivre.rocks/en/latest/usage/web-ui.html#)
- [安装教程](https://www.freebuf.com/sectool/92179.html)
- mkdir -m 1777 var_lib_mongodb var_log_mongodb ivre-share
- docker-compose up -d 

## Vagrant-centos7 安装指南
- [Vagrantfile](https://raw.githubusercontent.com/cea-sec/ivre/master/docker/Vagrantfile)
- rpm -ivh https://releases.hashicorp.com/vagrant/2.2.5/vagrant_2.2.5_x86_64.rpm
- vagrant up  --no-parallel
- [client安装教程](https://doc.ivre.rocks/en/latest/install/installation.html#)

## 容器清理
- docker ps -a | grep ivre | awk '{print $1}' | xargs docker stop | xargs docker rm
- /usr/local/share/ivre/geoip 这个里面执行 `` 国内下载比较耗时

## Docker 一步步使用
```bash
# https://hub.docker.com/_/mongo
 docker run -itd --name=mgdb --net=host -v /srv/docker/mongo/data:/data/db mongo 
 
 docker run -itd --name=ivrecli \
 --net=host --restart=always  \
 -v /etc/localtime:/etc/localtime:ro \
 ivre/client
 
 docker run -itd --restart=always --name=web --net=host ivre/web 
```

## ivrecli 运行
```bash 

yes | ivre ipinfo --init
yes | ivre scancli --init
yes | ivre view --init
yes | ivre flowcli --init
yes | ivre runscansagentdb --init
ivre ipdata --download --import-all
# 扫描
ivre runscans --routable --limit 1000 --output=XMLFork
ivre scan2db -c ROUTABLE,ROUTABLE-CAMPAIGN-001 -s MySource -r scans/ROUTABLE/up
ivre db2view nmap

```