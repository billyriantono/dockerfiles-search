FROM alpine:3.3


RUN echo "@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

RUN  apk add --update daemontools@testing openssl curl

ADD  /root /
RUN  chmod a+x /usr/local/sbin/*

#RUN  chmod a+x /etc/services/*/run

CMD  /usr/bin/svscan /etc/services
