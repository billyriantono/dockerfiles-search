FROM ubuntu:bionic

RUN apt-get update && \
    apt-get install -y syslog-ng && \
    apt-get autoremove -y -qq && \
    apt-get autoclean -y -qq && \
    rm -rf /var/lib/apt/lists/* 

ADD ./syslog-ng.conf /etc/syslog-ng/syslog-ng.conf

EXPOSE 514/udp
EXPOSE 601/tcp

ENTRYPOINT ["/usr/sbin/syslog-ng", "-F", "-d"]
