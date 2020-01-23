FROM phusion/baseimage:0.9.18

CMD ["/sbin/my_init"]

RUN apt-get update && \
    apt-get install -y python aptitude && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
