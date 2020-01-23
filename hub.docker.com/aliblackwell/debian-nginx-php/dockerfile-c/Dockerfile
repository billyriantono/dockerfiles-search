FROM ubuntu:14.04

#RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh

ENV HOME /root

#CMD ["/sbin/my_init"]

#RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y  build-essential  tcl wget

RUN wget http://download.redis.io/redis-stable.tar.gz -O - | tar -xvz

# RUN tar -zvzf /redis/redis-stable.tar.gz
RUN (cd /redis-stable && make)

RUN 	sed -i 's@bind 127.0.0.1@bind 0.0.0.0@' /redis-stable/redis.conf && \
	sed -i 's@daemonize yes@daemonize no@' /redis-stable/redis.conf && \
	sed -i 's@dir ./@dir /var/lib/redis@' /redis-stable/redis.conf

ENTRYPOINT ["/redis-stable/src/redis-server"]

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
