FROM kingedgar/baseimage-alpine

LABEL maintainer="kingedgar@gmail.com"
RUN apk update && \
	apk add --no-cache --update bash && \
	apk add --no-cache --update aria2

RUN apk --update add \
  ca-certificates \
  ruby \
  ruby-bundler \
  ruby-xmlrpc \
  ruby-dev && \
  rm -fr /usr/share/ri

ADD root/ /

RUN chmod -v +x /etc/services.d/*/run /etc/cont-init.d/*

VOLUME ["/download"]
VOLUME ["/config"]
EXPOSE 6800
