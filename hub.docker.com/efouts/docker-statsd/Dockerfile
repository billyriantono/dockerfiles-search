# Dockerfile for statsd
#
# VERSION               2

from    ubuntu:14.04
run     echo "deb http://archive.ubuntu.com/ubuntu quantal main universe" > /etc/apt/sources.list
run     apt-get -y update
run     apt-get -y install wget git python
run     wget -O /tmp/node-v0.10.28.tar.gz http://nodejs.org/dist/v0.10.28/node-v0.10.28.tar.gz
run     tar -C /usr/local/ --strip-components=1 -zxvf /tmp/node-v0.10.28.tar.gz
run     rm /tmp/node-v0.10.28.tar.gz
run     git clone -b v0.7.1 git://github.com/etsy/statsd.git statsd

add     ./config.js ./statsd/config.js

expose  8125/udp
expose  8126/tcp

cmd     /usr/local/bin/node /statsd/stats.js /statsd/config.js
