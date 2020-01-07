FROM alpine:edge

RUN apk update \
    && apk upgrade \
    && apk add bash openssh-client \
    && sed -i -e "s/bin\/ash/bin\/bash/" /etc/passwd

ENV LC_ALL=en_US.UTF-8

WORKDIR /root
