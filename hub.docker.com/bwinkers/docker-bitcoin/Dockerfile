FROM alpine:3.6

MAINTAINER Brian Winkers <bwinkers@gmail.com>

RUN apk add --update --no-cache bitcoin

ENV HOME /bitcoin

ADD ./bin /usr/local/bin
RUN chmod a+x /usr/local/bin/*

VOLUME ["/bitcoin"]
EXPOSE 8332 8333
WORKDIR /bitcoin

ENTRYPOINT ["/usr/local/bin/docker_entrypoint.sh"]
