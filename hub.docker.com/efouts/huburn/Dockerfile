FROM ubuntu:14.04
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y update
RUN apt-get -y install software-properties-common

RUN add-apt-repository -y ppa:chris-lea/node.js
RUN apt-get -y update

RUN apt-get install -y git nodejs supervisor
RUN apt-get install --only-upgrade -y bash

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 8080

CMD ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
