FROM alpine

RUN apk add --no-cache beanstalkd

CMD ["/usr/bin/beanstalkd", "-b", "/var/lib/beanstalkd/binlog"]
