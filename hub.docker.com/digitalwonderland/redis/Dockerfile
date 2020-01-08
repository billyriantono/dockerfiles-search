# Redis

FROM digitalwonderland/base:latest

RUN yum install -y gcc make tar tcl && yum clean all \
  && curl -LsS https://github.com/antirez/redis/archive/3.0.0-rc1.tar.gz | tar -xzf - -C /tmp \
  && chown -R root:root /tmp/redis-* \
  && cd /tmp/redis-* \
  && make \
  && make test \
  && make install \
  && mkdir -p /etc/redis \
  && cp -f *.conf /etc/redis \
  && rm -rf /tmp/redis-*

RUN groupadd -r redis \
  && useradd -c "Redis" -d /var/lib/redis -g redis -m -r -s /sbin/nologin redis \
  && rm /var/lib/redis/.bash*

USER redis

EXPOSE 6379

VOLUME ["/var/lib/redis"]

WORKDIR /var/lib/redis

CMD ["redis-server", "/etc/redis/redis.conf"]
