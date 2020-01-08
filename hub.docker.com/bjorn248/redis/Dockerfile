FROM redis
MAINTAINER Bjorn Stange <bjorn248@gmail.com>

ADD redis.conf /etc/redis.conf

RUN chown redis:redis /etc/redis.conf

CMD [ "redis-server", "/etc/redis.conf" ]
