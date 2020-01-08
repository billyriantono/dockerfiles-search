FROM alpine:latest

MAINTAINER vincentliao <vincentliao@gmail.com>

RUN apk add --no-cache python3
RUN pip3 install --upgrade pip \
    && pip3 install python-gitlab

CMD ["/bin/sh"]
