FROM alpine:latest
MAINTAINER custa <custa@126.com>

ENV REFRESHED_AT 2017-10-10

RUN apk update && apk add py-pip && pip install --upgrade pip
RUN pip install shadowsocks

ADD run.sh /run.sh
RUN chmod +x /run.sh

EXPOSE 8388

ENTRYPOINT ["/run.sh"]
