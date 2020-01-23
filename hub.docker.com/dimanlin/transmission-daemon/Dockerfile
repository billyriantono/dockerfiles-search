FROM alpine:3.9

MAINTAINER dimanlin

RUN apk add --no-cache --no-progress transmission-daemon && \
    mkdir /transmission && \
    mkdir /transmission/watch && \
    mkdir /transmission/incomplete && \
    mkdir /transmission/log && \
    mkdir /transmission/config && \
    mkdir /transmission/download && \
    mkdir /transmission/pids

COPY init.sh /

EXPOSE 51413
EXPOSE 9091

VOLUME ["/transmission"]

CMD ["/init.sh"]

