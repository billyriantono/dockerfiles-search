# VERSION 1.0
# DOCKER-VERSION  1.2.0 and up
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    Redis Image Container

FROM dockerbase/service

# Run dockerbase script
ADD     redis.sh /dockerbase/
RUN     /dockerbase/redis.sh

RUN     mkdir -p /etc/service/redis
ADD     build/runit/redis /etc/service/redis/run

EXPOSE  6379
