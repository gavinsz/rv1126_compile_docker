#1 install docker and docker-compose
sudo apt-get install  docker docker-compose -y

#2 设置非root账号不用sudo直接执行docker命令
sudo groupadd docker
sudo gpasswd -a ${USER} docker
sudo systemctl restart docker
sudo chmod a+rw /var/run/docker.sock

#3导入image
docker load < h7_compile.tar.gz

#4 设定docker映射的文件夹, 修改docker-compose.yml
#将/home/xxx/work这个目录映射到docker容器中的/home/work
 - /home/xxx/work:/home/work

#5 启动h7_compile容器
docker-compose up -d

#6 进入docker
docker exec -ti h7_compile /bin/bash
cd /home/work/BaiLing_rv1126_mainboard_h7_sdk
./build.sh 