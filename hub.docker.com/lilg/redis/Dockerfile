FROM redis:alpine
MAINTAINER lilg <lilg@asiainfo.com>

RUN apk add --no-cache --update-cache --update supervisor && \
    rm -rf /tmp/* /var/cache/apk/* 

ADD supervisord.conf /etc/supervisord.conf
ADD sentinel.conf /redis/conf/sentinel.conf

RUN chown -R redis:redis /redis

EXPOSE 6379
EXPOSE 26379
CMD [ "supervisord","-n","-c","/etc/supervisord.conf"]]
