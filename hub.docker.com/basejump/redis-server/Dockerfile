### Dockerfile
#
# Redis

FROM basejump/build-base
MAINTAINER Devon Weller <dweller@atlasworks.com>

RUN yum install -y redis

# Expose ports
EXPOSE      6379

# run redis server
ENTRYPOINT  ["/usr/sbin/redis-server"]

