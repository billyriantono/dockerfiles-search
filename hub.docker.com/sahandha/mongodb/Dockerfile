FROM mongo

MAINTAINER Sahand Hariri sahandha@gmail.com

RUN sed -i 's/bindIp: 127.0.0.1/#bindIp: 0.0.0.0/g' /etc/mongod.conf.orig
RUN apt-get install -y vim; exit 0

RUN chmod 777 /data/db
