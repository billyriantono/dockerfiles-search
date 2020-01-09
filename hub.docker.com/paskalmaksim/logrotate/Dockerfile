FROM alpine:3.10

RUN apk --update add logrotate \
  && echo "* * * * * /usr/sbin/logrotate /conf/logrotate.conf" >> /etc/crontabs/root

ADD logrotate.conf /conf/logrotate.conf

CMD ["crond", "-f"]