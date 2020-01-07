FROM alpine:3.6

MAINTAINER Willian Cardoso <wvcardoso@gmail.com>

RUN apk update
RUN apk add --no-cache mongodb && rm /usr/bin/mongoperf

VOLUME /data/db
EXPOSE 27017 28017

COPY exec.sh /root

ENTRYPOINT [ "/root/exec.sh" ]
CMD [ "mongod", "--bind_ip", "0.0.0.0" ]
