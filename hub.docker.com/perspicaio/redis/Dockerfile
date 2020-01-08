FROM alpine:latest

# Install redis
RUN echo "http://dl-4.alpinelinux.org/alpine/v3.1/main" >> /etc/apk/repositories
RUN apk add --update redis=2.8.23-r0 && rm -rf /var/cache/apk/*
RUN apk add --update bash && rm -rf /var/cache/apk/*
RUN mkdir /data && chown -R redis:redis /data
#RUN echo -e "include /etc/redis-local.conf\n" >> /etc/redis.conf

# Add the files
#ADD root /

VOLUME ["/data"]

# Expose the ports for redis
EXPOSE 6379
ENTRYPOINT ["/usr/bin/redis-server"]
CMD ["--port 6379", "--loglevel verbose"]
#ENTRYPOINT /bin/bash
