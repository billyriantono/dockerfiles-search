FROM centos:7
MAINTAINER Jianghg <jianghg@jiaziworld.com>

ENV MEMCACHED_VERSION 1.4.33 
ENV REDIS_VERSION 2.8.19

# Layer 5
ADD files/ /tmp/files/
# Layer 6
RUN set -x && \
#
#yum install -y gcc gcc-c++ make libevent-devel tcl python-setuptools --downloadonly --downloaddir=/data  && \
cd /tmp/files/RPMs && \
rpm -ivh *.rpm && \
#
mkdir -p /data/redis && \
mkdir -p /opt/redis/etc && \
mkdir -p /data/logs/{redis,memcached} && \
mkdir -p /var/run/{sshd,supervisord} && \
tar xf /tmp/files/memcached-${MEMCACHED_VERSION}.tar.gz -C /tmp/files/ && \
tar xf /tmp/files/redis-${REDIS_VERSION}.tar.gz -C /tmp/files/ && \
cp -f /tmp/files/busybox-x86_64 /usr/bin/busybox && \
cp -f /tmp/files/redis.conf /opt/redis/etc/redis.conf && \
cp -f /tmp/files/start.sh /start.sh && \
#
#Install supervisor
easy_install supervisor && \
cp -f /tmp/files/supervisord.conf /etc/supervisord.conf && \
#
cd /tmp/files/memcached-${MEMCACHED_VERSION} && \
./configure --prefix=/opt/memcached && \
make && make install && \
cd /tmp/files/redis-${REDIS_VERSION} && \
make PREFIX=/opt/redis install

VOLUME ["/data/redis","/data/logs"]
EXPOSE 6379 11211
ENTRYPOINT ["/start.sh"]


