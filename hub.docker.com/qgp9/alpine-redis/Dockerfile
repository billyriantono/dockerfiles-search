FROM alpine
MAINTAINER qgp9 <qgp9@rm-rf.work>

# BASE SET
RUN apk update && apk upgrade && apk update
RUN apk add --update bash && rm -rf /var/cache/apk/*  

# ADDITIONAL SET

# REDIS
RUN apk add --update redis && rm -rf /var/cache/apk/*  

VOLUME  /data
WORKDIR /data

ADD ./sample.redis.conf /etc/redis.conf

EXPOSE 6379

CMD ["redis-server", "/etc/redis.conf"]
