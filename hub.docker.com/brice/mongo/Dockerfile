FROM ubuntu:12.10
MAINTAINER Brandon Rice <brice84@gmail.com>

RUN apt-get update
RUN apt-get -y upgrade

# Because docker replaces /sbin/init: https://github.com/dotcloud/docker/issues/1025 
RUN dpkg-divert --local --rename --add /sbin/initctl
RUN ln -s /bin/true /sbin/initctl
RUN mkdir -p /data/db
RUN apt-get -y install mongodb-server

EXPOSE 27017

VOLUME ["/var/lib/mongodb"]
CMD ["mongod"]