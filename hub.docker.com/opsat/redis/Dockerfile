FROM opsat/base:latest

MAINTAINER "Serban TEODORESCU <teodorescu.serban@gmail.com>"

#COPY run_redis redis.conf /
COPY run_redis /

RUN apk add --update-cache redis && \
    rm -rf /var/cache/apk/* && \
    mkdir -p /etc/redis /etc/services.d/redis && \
    mv /run_redis /etc/services.d/redis/run
    #  && \
    # mv /etc/redis.conf /etc/redis.conf.ini && \
    # mv /redis.conf /etc/redis/

EXPOSE 6379

VOLUME /var/log/redis /var/lib/redis /etc/redis
