FROM phusion/baseimage:0.11
CMD ["/sbin/my_init"]

RUN mkdir /etc/service/keepalive
ADD keepalive.sh /etc/service/keepalive/run

RUN chmod +x /etc/service/*/run
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
