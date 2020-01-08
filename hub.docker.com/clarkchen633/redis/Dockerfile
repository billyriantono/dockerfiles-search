FROM clarkchen633/ubuntux64:14.04.5
MAINTAINER clarkchen633@gmail.com

# Add deb-src lines to make apt-get build-dep work.
RUN echo 'APT::Install-Recommends 0;' >> /etc/apt/apt.conf.d/01norecommends \
 && echo 'APT::Install-Suggests 0;' >> /etc/apt/apt.conf.d/01norecommends \
 && echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections \
 && echo "#!/bin/sh\nexit 0" > /usr/sbin/policy-rc.d \
 && cat /etc/apt/sources.list | sed "s/deb /deb-src /" >> /etc/apt/sources.list

# To get rid of error messages like "debconf: unable to initialize frontend: Dialog":
# Avoid ERROR: invoke-rc.d: policy-rc.d denied execution of start. 
# The system-wide cache is empty. You may want to run 'apt-file update' 
# RUN apt-file update
# Workaround apt-get giving frequent "Remote end closed connection" errors.
# See http://stackoverflow.com/a/37426929/4355276
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils apt-file \
 && apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y vim.tiny wget sudo net-tools ca-certificates unzip apt-transport-https curl
# && sed -i "s/httpredir.debian.org/`curl -s -D - http://httpredir.debian.org/demo/debian/ | awk '/^Link:/ { print $2 }' | sed -e 's@<http://\(.*\)/debian/>;@\1@g'`/" /etc/apt/sources.list
# && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV REDIS_USER=redis \
    REDIS_DATA_DIR=/var/lib/redis \
    REDIS_LOG_DIR=/var/log/redis

RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y redis-server \
 && sed 's/^daemonize yes/daemonize no/' -i /etc/redis/redis.conf \
 && sed 's/^bind 127.0.0.1/bind 0.0.0.0/' -i /etc/redis/redis.conf \
 && sed 's/^# unixsocket /unixsocket /' -i /etc/redis/redis.conf \
 && sed 's/^# unixsocketperm 755/unixsocketperm 777/' -i /etc/redis/redis.conf \
 && sed '/^logfile/d' -i /etc/redis/redis.conf \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY entrypoint.sh /sbin/entrypoint.sh
RUN chmod 755 /sbin/entrypoint.sh

EXPOSE 6379/tcp
VOLUME ["${REDIS_DATA_DIR}"]
ENTRYPOINT ["/sbin/entrypoint.sh"]
