#FROM debian:wheezy
FROM debian:latest
ENV DEBIAN_FRONTEND noninteractive
MAINTAINER  Etienne Lachance <el@elcweb.ca>

RUN apt-get update && apt-get -y dist-upgrade && \
    apt-get -y install automysqlbackup && \
    apt-get -y install ssmtp && \
    apt-get -y purge exim4*

ADD run.sh /run.sh
ADD automysqlbackup.default /etc/default/automysqlbackup
CMD ["/run.sh"]
