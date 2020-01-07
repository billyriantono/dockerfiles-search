#
# Redis Container
#

FROM alpine
MAINTAINER jurinva <jurinva@gmail.com>

# Update System and Install Redis
RUN apk update && apk add redis

# Volumes
#VOLUME /data

#WORKDIR /tmp/data

# Ports
#EXPOSE 6379

# Run Command
ENTRYPOINT ["/usr/bin/redis-server", "/etc/redis.conf"]


