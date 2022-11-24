# docker-project

## 青龙

```
docker run -dit \
-v $PWD/ql:/ql/data \
-v $PWD/ql/jbot:/ql/data/jbot \
-p 5700:5700 \
-e ENABLE_HANGUP=false \
-e ENABLE_WEB_PANEL=true \
--name qinglong \
--hostname qinglong \
--restart always \
whyour/qinglong:latest

docker run -dit \
-v $PWD/ql2:/ql/data \
-v $PWD/ql2/jbot:/ql/data/jbot \
-p 8888:5700 \
-e ENABLE_HANGUP=false \
-e ENABLE_WEB_PANEL=true \
--name ql \
--hostname ql \
--restart always \
whyour/qinglong:latest

docker run -dit \
-v $PWD/ql3:/ql/data \
-v $PWD/ql3/jbot:/ql/data/jbot \
-p 8899:5700 \
-e ENABLE_HANGUP=false \
-e ENABLE_WEB_PANEL=true \
--name wskey \
--hostname wskey \
--restart always \
whyour/qinglong:latest
```

## 机器人菜单
```
更新并重启青龙-->ql update
更新脚本-->ql extra
获取互助码-->ql code
资产查询-->task jd_task_assets.js now
京豆统计-->task ccwav_QLScript2/bot_jd_bean_change.js now
重置登录次数-->ql resetlet 
禁用两步验证-->ql resettfa
```
## 修复青龙白屏

```
进青龙容器docker exec -it qinglong bash  运行wget https://gitee.com/suiyuehq/ziyong/raw/master/ql_cdn/v2.10.13/bpxf.sh  最后运行bash bpxf.sh 看提示选1修复
```

## 解决青龙更新无法进入
```
容器内执行命令
mkdir -p /run/nginx
nginx -c /etc/nginx/nginx.conf
```

## 自动更新watchtower

```
运行一次即退出版
sudo docker create \
--name watchtower_dev_run_once \
-e TZ=Asia/Shanghai \
-v /var/run/docker.sock:/var/run/docker.sock \
containrrr/watchtower:latest-dev --cleanup --run-once

后台长期运行版
docker run -d \
--name watchtower_dev \
--restart=always \
-e TZ=Asia/Shanghai \
-e WATCHTOWER_CLEANUP=true \
-e WATCHTOWER_NOTIFICATIONS=shoutrrr \
-v /var/run/docker.sock:/var/run/docker.sock \
-s "* 0 * * * *" \
containrrr/watchtower:latest-dev --cleanup

docker run -d \
   --name watchtower-dev \
  -e TZ=Asia/Shanghai \
   --restart always \
   -e WATCHTOWER_CLEANUP=true \
   -e WATCHTOWER_NOTIFICATIONS=shoutrrr \
   -e WATCHTOWER_NOTIFICATION_URL=telegram://1851512831:AAGECAYf08Q4kQxp8TmuANsEOv5UxHVlzqE@telegram?channels=518623298 \
   -v /var/run/docker.sock:/var/run/docker.sock \
     containrrr/watchtower:latest  -c\
  -s "* 0 * * * *" \
$(cat ~/.watchtower.list)

docker run -d \
   --name watchtower-dev \
  -e TZ=Asia/Shanghai \
   --restart always \
   -e WATCHTOWER_CLEANUP=true \
   -e WATCHTOWER_NOTIFICATIONS=shoutrrr \
   -v /var/run/docker.sock:/var/run/docker.sock \
     containrrr/watchtower:latest  -c\
  -s "* */30 * * * *" \
$(cat ~/.watchtower.list)

docker run -d \
   --name watchtower-dev \
  -e TZ=Asia/Shanghai \
   --restart always \
   -e WATCHTOWER_CLEANUP=true \
   -e WATCHTOWER_NOTIFICATIONS=shoutrrr \
   -e WATCHTOWER_NOTIFICATION_URL=telegram://1851512831:AAGECAYf08Q4kQxp8TmuANsEOv5UxHVlzqE@telegram?channels=518623298 \
   -v /var/run/docker.sock:/var/run/docker.sock \
    containrrr/watchtower:latest-dev  -c\
  -s "* */30 * * * *" \
$(cat ~/.watchtower.list)

docker run -d \
   --name watchtower-dev \
  -e TZ=Asia/Shanghai \
   --restart always \
   -e WATCHTOWER_CLEANUP=true \
   -e WATCHTOWER_NOTIFICATIONS=shoutrrr \
   -v /var/run/docker.sock:/var/run/docker.sock \
    containrrr/watchtower:latest-dev  -c\
  -s "* /30 * * * *" \
$(cat ~/.watchtower.list)
```

## 网络测速

```
docker run -d --name homebox --restart unless-stopped -p 3300:3300 p3terx/homebox
```

## Portainer 

```
* docker volume create portainer_data
* docker run -d -p 8000:8000 -p 9000:9000 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce
* docker run -d -p 8000:8000 -p 9000:9000 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v /volume1/docker/portainer/data:/data \
    portainer/portainer:latest
```

## nark

```
安装步骤
1 进群 找玛卡巴卡获取许可 
@NolanNarkbot  点击start后
在群里使用命令菜单/narksq@NolanNarkbot获取许可 
2 在群里发送/narksq@NolanNarkbot 获取到授权之后 改名为Nark.lic
3 mkdir /root/Ark  
4 cd /root/Ark && mkdir -p Config   
5 将授权文件放入/root/Ark/Config中 
6 将Config.json 文件放入/root/Ark/Config
7 建立 日志文件夹  cd /root/Ark && mkdir -p logfile 
8 cd /root/Ark 准备拉取启动容器
arm需要将latest 更换为arm 即可
sudo docker run   --name nark -p 5701:80  -d  -v  "$(pwd)"/Config:/app/Config \
-v  "$(pwd)"/logfile:/app/logfile  \
-it --privileged=true  nolanhzy/nark:arm 

sudo docker run   --name ark -p 5702:80  -d  -v  /opt/Ark/Config:/app/Config \
-v  /opt/Ark/logfile:/app/logfile  \
-it --privileged=true  nolanhzy/nark:arm 
更新
docker run --rm     -v /var/run/docker.sock:/var/run/docker.sock     containrrr/watchtower -c     --run-once     nark
```
## mosdns

```
docker run -d --name mosdns -p 5454:53/udp -p 5454:53/tcp -v /etc/mosdns:/etc/mosdns irinesistiana/mosdns:latest
```

## Docker安装nginx proxy manager

```
#国外鸡
* sudo curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

#国内鸡
* sudo curl -L https://get.daocloud.io/docker/compose/releases/download/1.25.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

#添加可执行权限
* sudo chmod +x /usr/local/bin/docker-compose

#测试安装结果
* docker-compose --version
```

