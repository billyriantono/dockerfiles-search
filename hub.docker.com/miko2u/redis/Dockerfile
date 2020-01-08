FROM miko2u/centos7
MAINTAINER miko@cafelounge.net

RUN cd /tmp \
 && yum -y update \
 && yum -y install epel-release sudo \
 && yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm \
 && yum -y --enablerepo=remi install redis \
 && yum -y --enablerepo=remi clean all \
 && rm -rf /var/tmp/* /var/lib/yum/* /var/cache/yum/* \
 && find / -xdev -group redis -exec chgrp 496 {} \; && groupmod -g 496 redis \
 && find / -xdev -user redis -exec chown 496 {} \; && usermod -u 496 redis \
 && sed -e "s/^bind 127.0.0.1/bind 0.0.0.0/g" -i.dist /etc/redis.conf \
 && printf '#!/bin/sh\n\
/usr/bin/redis-cli info replication\n\
' > /usr/bin/redis-check \
 && printf '#!/bin/sh\n\
/usr/bin/redis-cli -p 26379 info sentinel\n\
' > /usr/bin/redis-check-sentinel \
 && chmod 755 /usr/bin/redis-check*


COPY reconfig.sh /etc/redis/
COPY redis-sentinel.conf /etc/
RUN printf '#\n\
Defaults:redis		!requiretty\n\
#\n\
redis	ALL=(ALL)	NOPASSWD:/sbin/ip,NOPASSWD:/sbin/arping\n\
' > /etc/sudoers.d/redis \
 && chmod 440 /etc/sudoers.d/redis \
 && chown redis:root /etc/redis-sentinel.conf

# volume
WORKDIR /root
VOLUME /var/lib/redis

# init
COPY init prepare /boot/
ENTRYPOINT ["/boot/init"]

# expose
EXPOSE 6379
