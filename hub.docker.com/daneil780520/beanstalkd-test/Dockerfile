FROM alpine:3.7
MAINTAINER ski2004 

RUN apk add --no-cache beanstalkd

EXPOSE 11300
ENTRYPOINT ["/usr/bin/beanstalkd"]
