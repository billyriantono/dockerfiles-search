FROM debian:jessie

MAINTAINER Bruce Lam <yplam@yplam.com>

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install wget build-essential libwrap0-dev libssl-dev python-distutils-extra libc-ares-dev uuid-dev libmysqlclient-dev unzip -y
RUN mkdir -p /usr/local/src
WORKDIR /usr/local/src
RUN wget http://mosquitto.org/files/source/mosquitto-1.4.5.tar.gz
RUN tar xvzf ./mosquitto-1.4.5.tar.gz
WORKDIR /usr/local/src/mosquitto-1.4.5
RUN make
RUN make install
RUN adduser --system --disabled-password --disabled-login mosquitto

WORKDIR /usr/local/src
RUN wget --no-check-certificate --quiet https://github.com/jpmens/mosquitto-auth-plug/archive/master.zip

RUN unzip ./master.zip
WORKDIR /usr/local/src/mosquitto-auth-plug-master
COPY Make/mosquitto_auth_plug/config.mk ./
RUN make

COPY mosquitto /etc/mosquitto
VOLUME ["/etc/mosquitto/"]

EXPOSE 1883
CMD ["/usr/local/sbin/mosquitto", "-c", "/etc/mosquitto/mosquitto.conf"]
