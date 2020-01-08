FROM nerelohw/docker-alpine:3.8

RUN apk add --no-cache redis \
&& rm -rf /var/cache/apk/*

EXPOSE 6379

CMD ["redis-server"]
