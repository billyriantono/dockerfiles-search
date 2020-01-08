FROM ubuntu:14.04

MAINTAINER Satoshi Yazawa https://github.com/yacchin1205/

# install dependencies
RUN apt-get update && apt-get install -y curl

RUN mkdir /etc/gate
ADD https://github.com/typester/gate/releases/download/v0.4/gate_0.4_linux_amd64.tar.gz /tmp/gate.tar.gz
RUN tar zxf /tmp/gate.tar.gz -C /tmp/
RUN mv /tmp/gate_0.4_linux_amd64 /usr/local/gate
RUN mkdir /usr/local/gate/www
ADD www /usr/local/gate/www

EXPOSE 443

CMD /usr/local/gate/gate -conf=/etc/gate/config.yml
