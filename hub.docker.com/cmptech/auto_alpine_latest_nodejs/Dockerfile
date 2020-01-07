FROM alpine:latest

Maintainer Wanjo Chan ( http://github.com/wanjochan/ )

# add bash
#RUN apk update && apk upgrade && apk add bash

# add nodejs
#RUN apk add --no-cache nodejs || (sed -i -e 's/dl-cdn/dl-4/g' /etc/apk/repositories && apk add --no-cache nodejs)
RUN sed -i -e 's/dl-cdn/dl-4/g' /etc/apk/repositories && apk add --no-cache nodejs \
&& apk --no-cache add ca-certificates openssl \
&& wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub \
&& apk --no-cache -X http://apkproxy.heroku.com/sgerrand/alpine-pkg-glibc add glibc glibc-bin \
&& rm -rf /var/cache/apk/ && mkdir /var/cache/apk && rm -rf /tmp/*

