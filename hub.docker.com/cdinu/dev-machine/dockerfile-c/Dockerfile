FROM alpine:3.2
RUN echo "http://dl-2.alpinelinux.org/alpine/v3.2/main" > /etc/apk/repositories
RUN apk update && apk add bash curl && rm -rf /var/cache/apk/*
ADD expandenv.sh /usr/local/bin/expandenv.sh
RUN chmod a+x /usr/local/bin/expandenv.sh
