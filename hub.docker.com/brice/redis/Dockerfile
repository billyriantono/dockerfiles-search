FROM ubuntu:12.10
MAINTAINER Brandon Rice <brice84@gmail.com>

RUN apt-get update
RUN apt-get -y upgrade

RUN apt-get -y install redis-server

EXPOSE 6317

CMD ["redis-server"]
