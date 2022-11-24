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
```
## 自动更新watchtower
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
