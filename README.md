# docker-project

## 域名自动续费
```
docker run -d \
--name freenom \
--restart always \
-v /root/freenom:/conf \
-v /root/freenom/logs:/app/logs \
-e RUN_AT="15 */3 * * *" \
luolongfei/freenom
```
```
docker run -d --name freenom --restart always -v $(pwd):/conf -v $(pwd)/logs:/app/logs -e RUN_AT="15 */3 * * *" \ luolongfei/freenom
```

## Portainer CE安装
```
docker volume create portainer_data
```
```
docker run -d -p 8000:8000 -p 9000:9000 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce
```
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
```

```
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
```

```
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
自定义版本：whyour/qinglong:2.13.8

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
##运行一次即退出版
```
```
sudo docker create \
--name watchtower_dev_run_once \
-e TZ=Asia/Shanghai \
-v /var/run/docker.sock:/var/run/docker.sock \
containrrr/watchtower:latest-dev --cleanup --run-once
```

```
##后台长期运行版
```
```
docker run -d \
--name watchtower_dev \
--restart=always \
-e TZ=Asia/Shanghai \
-e WATCHTOWER_CLEANUP=true \
-e WATCHTOWER_NOTIFICATIONS=shoutrrr \
-v /var/run/docker.sock:/var/run/docker.sock \
-s "* 0 * * * *" \
containrrr/watchtower:latest-dev --cleanup
```

```
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
```

```
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
```

```
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
```

```
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
docker volume create portainer_data
```
```
docker run -d -p 8000:8000 -p 9000:9000 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce
```
```
docker run -d -p 8000:8000 -p 9000:9000 --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v /volume1/docker/portainer/data:/data \
    portainer/portainer:latest
```

## nark

```
安装步骤
* 进群 找玛卡巴卡获取许可 
@NolanNarkbot  点击start后
在群里使用命令菜单/narksq@NolanNarkbot获取许可 
* 在群里发送/narksq@NolanNarkbot 获取到授权之后 改名为Nark.lic
* mkdir /root/Ark  
* cd /root/Ark && mkdir -p Config   
* 将授权文件放入/root/Ark/Config中 
* 将Config.json 文件放入/root/Ark/Config
* 建立 日志文件夹  cd /root/Ark && mkdir -p logfile 
* cd /root/Ark 准备拉取启动容器
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
## Pro部署教程
```
1 找 @NolanNarkbot  点击start
2 群里发送 /check@NolanNarkbot  再找 @NolanNarkbot           获取ProId
3 群里发送 pro签到          获取wskey使用次数（因为是内测阶段28号之前有效）
4 mkdir /root/pro        创建映射文件夹
5 cd /root/pro              进入文件夹
6 sudo docker run -id \
--name pro -p 5016:5016 \
-v "$(pwd)":/app/Data \
-e Prolic=第2步获取的 \
-e User=自定义管理帐号 \
-e Pwd=自定义管理密码(八位以上包含大小写字母、数字或特殊字符) \
--privileged=true \
nolanhzy/pro                                     
创建容器
6 进入 IP:5016               回车查看面板是否正常
7 进入 IP:5016/#/admin  进入管理界面

注：修改密码可以改文件夹中的Config.json 不是改密码 还代理的话 建议使用后台全局配置去改 如果密码错了10 admin就会等半个小时  不想等直接docker restart pro
28号以前群里发送pro签到 内测 一共20次wskey 用完可以再次签到
每个人一共20次wskey
没用完每天不会重置，要把20次用完群里发 pro签到 才会重置20次
第一次部署的必须发送 pro签到 才能部署找玛卡巴卡获取proid

推送：
https://wxpusher.zjiecode.com/admin/main/wxuser/list

回调地址  http://外网pro地址/api/wxpusher
```
## mosdns

```
docker run -d --name mosdns -p 5454:53/udp -p 5454:53/tcp -v /etc/mosdns:/etc/mosdns irinesistiana/mosdns:latest
```

## elecv2p

```
docker run -dit \
--restart=always \
--name elecv2p \
-e TZ=Asia/Shanghai \
-p 8100:80 -p 8101:8001 -p 8102:8002 \
-v $PWD/elecv2p/JSFile:/usr/local/app/script/JSFile \
-v $PWD/elecv2p/Store:/usr/local/app/script/Store \
-v $PWD/elecv2p/rootCA:/usr/local/app/rootCA \
-v $PWD/elecv2p/Lists:/usr/local/app/script/Lists \
-v $PWD/elecv2p/Shell:/usr/local/app/script/Shell \
-v $PWD/elecv2p/efss:/usr/local/app/efss \
-e ENABLE_HANGUP=true \
-e ENABLE_WEB_PANEL=true \
--hostname elecv2p \
elecv2/elecv2p:latest
```

```
docker run -dit \
--restart=always \
--name elecv2p1 \
-e TZ=Asia/Shanghai \
-p 8300:80 -p 8301:8001 -p 8302:8002 \
-v $PWD/elecv2p1/JSFile:/usr/local/app/script/JSFile \
-v $PWD/elecv2p1/Store:/usr/local/app/script/Store \
-v $PWD/elecv2p1/rootCA:/usr/local/app/rootCA \
-v $PWD/elecv2p1/Lists:/usr/local/app/script/Lists \
-v $PWD/elecv2p1/Shell:/usr/local/app/script/Shell \
-v $PWD/elecv2p1/efss:/usr/local/app/efss \
-e ENABLE_HANGUP=true \
-e ENABLE_WEB_PANEL=true \
--hostname elecv2p1 \
elecv2/elecv2p:latest
```

```
docker run -dit \
--restart=always \
--name elecv2p2 \
-e TZ=Asia/Shanghai \
-p 8400:80 -p 8401:8001 -p 8402:8002 \
-v $PWD/elecv2p2/JSFile:/usr/local/app/script/JSFile \
-v $PWD/elecv2p2/Store:/usr/local/app/script/Store \
-v $PWD/elecv2p2/rootCA:/usr/local/app/rootCA \
-v $PWD/elecv2p2/Lists:/usr/local/app/script/Lists \
-v $PWD/elecv2p2/Shell:/usr/local/app/script/Shell \
-v $PWD/elecv2p2/efss:/usr/local/app/efss \
-e ENABLE_HANGUP=true \
-e ENABLE_WEB_PANEL=true \
--hostname elecv2p2 \
elecv2/elecv2p:latest
```

```
docker run -dit \
--restart=always \
--name elecv2p3 \
-e TZ=Asia/Shanghai \
-p 8500:80 -p 8501:8001 -p 8502:8002 \
-v $PWD/elecv2p3/JSFile:/usr/local/app/script/JSFile \
-v $PWD/elecv2p3/Store:/usr/local/app/script/Store \
-v $PWD/elecv2p3/rootCA:/usr/local/app/rootCA \
-v $PWD/elecv2p3/Lists:/usr/local/app/script/Lists \
-v $PWD/elecv2p3/Shell:/usr/local/app/script/Shell \
-v $PWD/elecv2p3/efss:/usr/local/app/efss \
-e ENABLE_HANGUP=true \
-e ENABLE_WEB_PANEL=true \
--hostname elecv2p3 \
elecv2/elecv2p:latest
```

## gocq

```
docker run --rm -it --name="gocq" -v $PWD/go-cqhttp:/data xzsk2/gocqhttp-docker:latest
```
```
docker run -d -it --name="gocq" -v $PWD/go-cqhttp:/data yanxsir/go-cqhttp:latest
```
更换镜像：jyishit/go-cqhttp:latest

## 安装docker-compose

#国外鸡
```
sudo curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```
#国内鸡
```
sudo curl -L https://get.daocloud.io/docker/compose/releases/download/1.25.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```
#添加可执行权限

```
sudo chmod +x /usr/local/bin/docker-compose
```
#测试安装结果

```
docker-compose --version
```
## Clash-mosdns
```
version: "3"
services:
  clash:
    image: dsmmyq/docker-clash
    volumes:
      - /root/clash:/clash_config
    restart: unless-stopped
    privileged: true
    networks:
      vlan:
        ipv4_address: 192.168.1.10
    container_name: clash
  clash1:
    image: metacubex/clash-meta:latest
    volumes:
      - /root/clash1:/root/.config/clash
    restart: unless-stopped
    privileged: true
    networks: 
      vlan:
        ipv4_address: 192.168.1.18
    container_name: clash 
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    restart: unless-stopped
    security_opt:
      - no-new-privileges:true
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ./portainer-data:/data
    ports:
      - 9000:9000    
networks:
  vlan:
    driver: macvlan
    driver_opts:
      parent: eth0 # 要桥接的网卡
    ipam:
      driver: default
      config:
        - subnet: "192.168.1.0/24" # 改成你的局域网的CIDR地址块
          gateway: 192.168.1.1 # 改成你的网关
```
      
## Nginx Proxy Manage
```
* 在主机新建一个文件夹
* 在文件夹内新建 docker-compose.yml 文件，填入以下代码
```
```
version: '3'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```
```
 * cd到文件所在位置，执行：docker-compose up -d
* 进入nginx proxy manager后台
* 后台地址：ip：81
* 初始账号密码
Email:    admin@example.com
Password: changeme
```

## 奥特曼
```
-p  autman端口   外部端口:docker内部端口写死
-v  挂载目录  本地目录:docker内部目录
```

## 方式1:挂载需要的部分 有点繁琐 下面是例子
```
docker run -d --name autman --restart always -p 9999:8080 -v /root/autman:/autMan hdbjlizhe/autman:latest
```

##【群晖docker命令】建议在volume1下新建autman文件夹
```
docker run -d --name autman --restart always -p 9999:8080 -v /volume1/autman:/autMan hdbjlizhe/autman:latest
```
## 方式2:docker-compose
/root/autMan为本地路径

```
version: '3'
services:
  autman:
    image: hdbjlizhe/autman:latest
    container_name: autman
    network_mode: bridge
    hostname: autman
    tty: true
    restart: always
    ports:
      - '8080:8080'
    volumes:
      - /root/autMan:/autMan
```
## 自动抓wskey到机器人
```
docker run -itd -v /root/wskey:/run/data -p 7878:8080 mzzsfy/proxy-support
```
## Frps/Frpc
教程：
```
https://zhuanlan.zhihu.com/p/579430608
```
下载地址：
```
https://github.com/fatedier/frp
```
```
docker run  -d \
--restart=always \
--network host \
-v /etc/frp/frps.ini:/etc/frp/frps.ini \
--name frps snowdreamtech/frps
```
```
docker run \
--restart=always \
--network host -d \
-v /etc/frp/frpc.ini:/etc/frp/frpc.ini \
--name frpc \
snowdreamtech/frpc
```

## linux上使用rclone挂载onedrive或googledrive并设置开机自启
安装Rclone一键脚本
```
curl https://rclone.org/install.sh | sudo bash
```
Rclone连接OneDrive获取token，Windows电脑上下载Rclone，然后解压，使用cmd进入解压后的文件夹输入命令
```
https://rclone.org/downloads/
```
```
rclone.exe authorize "onedrive"
```
MacOS电脑上下载Rclone安装，下载地址:
```
https://rclone.org/downloads/
```
```
rclone authorize "onedrive"
```
配置 Rclone,输入 rclone config 命令，会出现以下教程，参照下面的注释进行操作。
TIPS: 因为 RCLONE 会时不时进行更新，当你看到这篇教程时菜单选项可能已经发生了略微的改动，但大致思路不会变，不要无脑照搬操作。
```
#教程1
```
https://p3terx.com/archives/rclone-installation-and-configuration-tutorial.html
```
#教程2
```
https://www.eehello.com/?post=321
```

```
## 哪吒监控的透明主题
```
<style>
/* 屏幕适配 */
@media only screen and (min-width: 1200px) {
.ui.container {
width: 80% !important;
}
}
 
@media only screen and (max-width: 767px) {
.ui.card>.content>.header:not(.ui), .ui.cards>.card>.content>.header:not(.ui) {
    margin-top: 0.4em !important;
}
}
 
/* 整体图标 */
i.icon {
color: #000;
width: 1.2em !important;
}
 
/* 背景图片 */
body {
content: " " !important;
background: fixed !important;
z-index: -1 !important;
top: 0 !important;
right: 0 !important;
bottom: 0 !important;
left: 0 !important;
background-position: top !important;
background-repeat: no-repeat !important;
background-size: cover !important;
background-image: url(https://cdn.jsdelivr.net/gh/lonelypers/Img@main/20211024/dc82125bc942e2c9cc63b245cd001764/dc82125bc942e2c9cc63b245cd001764.webp) !important;
font-family: Arial,Helvetica,sans-serif !important;
}
 
/* 导航栏 */
.ui.large.menu {
border: 0 !important;
border-radius: 0px !important;
background-color: rgba(255, 255, 255, 55%) !important;
}
 
/* 首页按钮 */
.ui.menu .active.item {
background-color: transparent !important;
}
 
/* 导航栏下拉框 */
.ui.dropdown .menu {
border: 0 !important;
border-radius: 0 !important;
background-color: rgba(255, 255, 255, 80%) !important;
}
 
/* 登陆按钮 */
.nezha-primary-btn {
background-color: transparent !important;
color: #000 !important;
}
 
/* 大卡片 */
#app .ui.fluid.accordion {
background-color: #fbfbfb26 !important;
border-radius: 0.4rem !important;
}
 
/* 小卡片 */
.ui.four.cards>.card {
border-radius: 0.6rem !important;
background-color: #fafafaa3 !important;
}
 
.status.cards .wide.column {
padding-top: 0 !important;
padding-bottom: 0 !important;
height: 3.3rem !important;
}
 
.status.cards .three.wide.column {
padding-right: 0rem !important;
}
 
.status.cards .wide.column:nth-child(1) {
margin-top: 2rem !important;
}
 
.status.cards .wide.column:nth-child(2) {
margin-top: 2rem !important;
}
 
.status.cards .description {
padding-bottom: 0 !important;
}
 
/* 小鸡名 */
.status.cards .flag {
margin-right: 0.5rem !important;
}
 
/* 弹出卡片图标 */
.status.cards .header > .info.icon {
margin-right: 0 !important;
}
 
.nezha-secondary-font {
color: #21ba45 !important;
}
 
/* 进度条 */
.ui.progress {
border-radius: 50rem !important;
}
 
.ui.progress .bar {
min-width: 1.8em !important;
border-radius: 15px !important;
line-height: 1.65em !important;
}
 
.ui.fine.progress> .bar {
background-color: #21ba45 !important;
}
 
.ui.progress> .bar {
background-color: #000 !important;
}
 
.ui.progress.fine .bar {
background-color: #21ba45 !important;
}
 
.ui.progress.warning .bar {
background-color: #ff9800 !important;
}
 
.ui.progress.error .bar {
background-color: #e41e10 !important;
}
 
.ui.progress.offline .bar {
background-color: #000 !important;
}
 
/* 上传下载 */
.status.cards .outline.icon {
margin-right: 1px !important;
}
 
 
i.arrow.alternate.circle.down.outline.icon
{
color: #21ba45 !important;
}
i.arrow.alternate.circle.up.outline.icon
 
 
{
color: red !important;
}
 
/* 弹出卡片小箭头 */
.ui.right.center.popup {
margin: -3px 0 0 0.914286em !important;
-webkit-transform-origin: left 50% !important;
transform-origin: left 50% !important;
}
 
.ui.bottom.left.popup {
margin-left: 1px !important;
margin-top: 3px !important;
}
 
.ui.top.left.popup {
margin-left: 0 !important;
margin-bottom: 10px !important;
}
 
.ui.top.right.popup {
margin-right: 0 !important;
margin-bottom: 8px !important;
}
 
.ui.left.center.popup {
margin: -3px .91428571em 0 0 !important;
-webkit-transform-origin: right 50% !important;
transform-origin: right 50% !important;
}
 
.ui.right.center.popup:before,
.ui.left.center.popup:before {
border: 0px solid #fafafaeb !important;
background: #fafafaeb !important;
}
 
.ui.top.popup:before {
border-color: #fafafaeb transparent transparent !important;
}
 
.ui.popup:before {
border-color: #fafafaeb transparent transparent !important;
}
 
.ui.bottom.left.popup:before {
border-radius: 0 !important;
border: 1px solid transparent !important;
border-color: #fafafaeb transparent transparent !important;
background: #fafafaeb !important;
-webkit-box-shadow: 0px 0px 0 0 
#fafafaeb !important;
box-shadow: 0px 0px 0 0 #fafafaeb !important;
-webkit-tap-highlight-color: rgba(0,0,0,0) !important;
}
 
.ui.bottom.right.popup:before {
border-radius: 0 !important;
border: 1px solid transparent !important;
border-color: #fafafaeb transparent transparent !important;
background: #fafafaeb !important
-webkit-box-shadow: 0px 0px 0 0 #fafafaeb !important;
box-shadow: 0px 0px 0 0 #fafafaeb !important;
-webkit-tap-highlight-color: rgba(0,0,0,0) !important;
}
 
.ui.top.left.popup:before {
border-radius: 0 !important;
border: 1px solid transparent !important;
border-color: #fafafaeb transparent transparent !important;
background: #fafafaeb !important;
-webkit-box-shadow: 0px 0px 0 0 #fafafaeb !important;
box-shadow: 0px 0px 0 0 #fafafaeb !important;
-webkit-tap-highlight-color: rgba(0,0,0,0) !important;
}
 
.ui.top.right.popup:before {
border-radius: 0 !important;
border: 1px solid transparent !important;
border-color: #fafafaeb transparent transparent !important;
background: #fafafaeb !important;
-webkit-box-shadow: 0px 0px 0 0 #fafafaeb !important;
box-shadow: 0px 0px 0 0 #fafafaeb !important;
-webkit-tap-highlight-color: rgba(0,0,0,0) !important;
}
 
.ui.left.center.popup:before {
border-radius: 0 !important;
border: 1px solid transparent !important;
border-color: #fafafaeb transparent transparent !important;
background: #fafafaeb !important;
-webkit-box-shadow: 0px 0px 0 0 #fafafaeb !important;
box-shadow: 0px 0px 0 0 #fafafaeb !important;
-webkit-tap-highlight-color: rgba(0,0,0,0) !important;
}
 
/* 弹出卡片 */
.status.cards .ui.content.popup {
min-width: 20rem !important;
line-height: 2rem !important;
border-radius: 5px !important;
border: 1px solid transparent !important;
background-color: #fafafaeb !important;
font-family: Arial,Helvetica,sans-serif !important;
}
 
.ui.content {
margin: 0 !important;
padding: 1em !important;
}
 
/* 服务页 */
.ui.table {
background: RGB(225,225,225,0.6) !important;
}
 
.ui.table thead th {
background: transparent !important;
}
 
/* 服务页进度条 */
.service-status .good {
background-color: #21ba45 !important;
}
 
.service-status .danger {
background-color: red !important;
}
 
.service-status .warning {
background-color: orange !important;
}
 
/* 版权 */
.ui.inverted.segment, 
.ui.primary.inverted.segment {
color: #000 !important;
font-weight: bold !important;
background-color: #fafafaa3 !important;
}
</style>
 
<!--Logo和版权-->
<script>
window.onload = function(){
var avatar=document.querySelector(".item img")
var footer=document.querySelector("div.is-size-7")
footer.innerHTML="渐行渐远"
footer.style.visibility="visible"
avatar.src="https://cdn.jsdelivr.net/gh/lonelypers/Jsdelivr-CDN@master/Akina/3.4.3/usr/themes/Akina/images/favicon.ico"
avatar.style.visibility="visible"
}
</script>
```
