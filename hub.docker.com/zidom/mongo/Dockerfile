FROM ubuntu:14.04
MAINTAINER Mohammad Zolfaghari <zidom72@gmail.com>

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist \
	10gen' | tee /etc/apt/sources.list.d/10gen.list
RUN apt-get update && apt-get install -y mongodb-org

RUN mkdir -p /data/db
RUN sed -i 's/bind_ip = 127.0.0.1/bind_ip = 0.0.0.0/' /etc/mongod.conf

EXPOSE 27017

CMD ["mongod"]
