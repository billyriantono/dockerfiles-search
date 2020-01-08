FROM feduxorg/centos:latest

MAINTAINER dev@fedux.org

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r redis && useradd -r -g redis redis

ENV REDIS_VERSION 3.2.5
ENV REDIS_DOWNLOAD_URL http://download.redis.io/releases/redis-${REDIS_VERSION}.tar.gz

# ADD redis.conf-sane-defaults.patch /tmp/

RUN buildDeps='gcc make glibc-devel patch' \
  && set -x \
  && yum install -y $buildDeps \
  && mkdir -p /usr/src/redis \
  && curl -sSL "$REDIS_DOWNLOAD_URL" -o redis.tar.gz \
  && tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1 \
  && rm redis.tar.gz \
#  && patch -p1 -i /tmp/redis.conf-sane-defaults.patch /usr/src/redis/redis.conf \
#  && rm /tmp/redis.conf-sane-defaults.patch \
  && make -C /usr/src/redis \
  && make -C /usr/src/redis PREFIX=/usr install \
  && cp /usr/src/redis/redis.conf /etc/redis.conf \
  && rm -r /usr/src/redis \
  && yum remove -y $buildDeps \
  && yum clean -y all

# Add systemd support
ADD redis.service /etc/systemd/system/redis.service
RUN systemctl enable redis.service

VOLUME /var/lib/redis
WORKDIR /var/lib/redis

EXPOSE 6379

# USER redis
