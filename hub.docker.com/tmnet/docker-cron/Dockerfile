FROM alpine:latest
MAINTAINER Mads Hvelplund <mhv@tmnet.dk>

VOLUME /var/spool/cron/crontabs

RUN touch /var/log/cron.log

CMD crond -l 6 -f -L /dev/stdout