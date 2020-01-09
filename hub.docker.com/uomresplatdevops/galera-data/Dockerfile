FROM busybox:latest
MAINTAINER Tim Dettrick <t.dettrick@uq.edu.au>

RUN addgroup -g 330 -S mysql && \
  adduser -u 330 -S -D -G mysql -h /data mysql

VOLUME /data
