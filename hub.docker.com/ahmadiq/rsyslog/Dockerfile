FROM phusion/baseimage:0.9.16
MAINTAINER Ahmad Iqbal <ahmad@aurorasolutions.io>

RUN add-apt-repository ppa:adiscon/v8-stable
RUN apt-get update && apt-get install -y -q rsyslog
RUN apt-get clean

EXPOSE 514/tcp 514/udp

CMD ["/usr/sbin/rsyslogd", "-n"]
