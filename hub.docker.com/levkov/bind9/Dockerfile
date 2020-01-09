FROM levkov/base:latest
MAINTAINER levkov

RUN apt-get update && apt-get install -y bind9

COPY conf/named.conf /etc/supervisor/conf.d/named.conf

EXPOSE 53/tcp 53/udp
