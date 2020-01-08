FROM usijo/docker-alpine
MAINTAINER Hongshun Yang<ojisucom@gmail.com>

RUN apk add --no-cache redis \
&& rm -rf /var/cache/apk/*

EXPOSE 6379

CMD ["redis-server"]
