from ubuntu:14.04
maintainer Kerwin Piao <piaoyuankui@gmail.com>

run apt-get clean all
run apt-get update
run apt-get install -y devscripts build-essential libssl-dev gawk m4 gcc-multilib

# install packages
run apt-get install -y build-essential libevent-dev libssl-dev wget 

# install 3rpoxy
workdir /usr/src
run wget http://3proxy.ru/0.7.1.1/3proxy-0.7.1.1.tgz && tar zxvf 3proxy-0.7.1.1.tgz

run echo '#define ANONYMOUS 1' >> /usr/src/3proxy/src/3proxy.h

workdir /usr/src/3proxy
run make -f Makefile.Linux
run make -f Makefile.Linux install

add ./start.sh /start.sh
add ./etc/3proxy.cfg /etc/3proxy.cfg

expose 5017
cmd /start.sh
