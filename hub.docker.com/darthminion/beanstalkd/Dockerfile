FROM alpine:latest

RUN cp /etc/apk/repositories /etc/apk/repositories.backup && \
    sed -i -E "s|http://.+/alpine|http://mirrors\.aliyun\.com/alpine|" /etc/apk/repositories && \
    apk add --no-cache beanstalkd

EXPOSE 11300

CMD ["beanstalkd", "-V"]
