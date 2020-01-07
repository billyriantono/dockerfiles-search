FROM alpine:3.5
MAINTAINER Tobias Gurtzick <magic@wizardtales.com>

RUN apk add --update --no-cache beanstalkd && rm -fr /var/cache/apk/* \
  && mkdir /data && chown nobody:nobody /data

EXPOSE 11300
VOLUME [ "/data" ]
ENTRYPOINT ["beanstalkd", "-p", "11300", "-u", "nobody", "-b", "/data"]
