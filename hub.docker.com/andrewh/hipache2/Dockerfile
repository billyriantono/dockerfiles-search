# DOCKER-VERSION 0.6.0

from  ubuntu:12.04

run mkdir /src
run mkdir -p /var/log/supervisor

run echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
run apt-get -y update

run apt-get -y install wget git redis-server supervisor

run wget -O - http://nodejs.org/dist/v0.8.26/node-v0.8.26-linux-x64.tar.gz | tar -C /usr/local/ --strip-components=1 -zxv
run npm install hipache -g

add ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf
add ./start-hipache.sh /src/start-hipache.sh

expose  80
expose  6379

cmd ["sh", "-ex", "/src/start-hipache.sh"]
