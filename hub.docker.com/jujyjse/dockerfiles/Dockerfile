FROM alpine:edge

RUN apk add netdata --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/
EXPOSE 19999
ENTRYPOINT ["/usr/sbin/netdata","-D","-s","/host"]
