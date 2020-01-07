FROM ubuntu:12.04

ENV DEBIAN_FRONTEND noninteractive

RUN locale-gen en_US.utf8

ENV LC_All en_US.utf8

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install wget -y

RUN groupadd -r mongodb && useradd -r -g mongodb mongodb

RUN mkdir -p /data/db /data/configdb \
	&& chown -R mongodb:mongodb /data/db /data/configdb

RUN cd / ;\
	wget http://downloads.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1204-2.7.8.tgz ;\
	tar -xvzf mongodb-linux-x86_64-ubuntu1204-2.7.8.tgz

RUN mv /mongodb-linux-x86_64-ubuntu1204-2.7.8 /mongodb

RUN export PATH=/mongodb/bin:$PATH

ENV DEBIAN_FRONTEND dialog

VOLUME /data/db /data/configdb

EXPOSE 27017
CMD ["/mongodb/bin/mongod"]
