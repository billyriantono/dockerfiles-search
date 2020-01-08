FROM ubuntu:xenial
MAINTAINER Anatoly Litovsky <anatolylit@gmail.com>
MAINTAINER Yair Zaslavsky <yair.zaslavsky@gmail.com>
ENV container docker
#TODO : make it auto detectable from inside

RUN apt-get clean && apt-get update 
RUN apt-get -y install python-pip

RUN pip install websockify

RUN mkdir /certs
VOLUME /certs

ENV CERT /certs/cert.pem
ENV KEY /certs/key.pem

RUN mkdir -p /mnt/locks
VOLUME /mnt/locks

COPY run.sh /run.sh
RUN chmod +x /run.sh

EXPOSE 6080

CMD ["/run.sh"]

