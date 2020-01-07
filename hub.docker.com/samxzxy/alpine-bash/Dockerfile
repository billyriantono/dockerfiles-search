# alpine-bash

FROM samxzxy/alpine-base:3.4
MAINTAINER Sam ccopsuse#g!.com

RUN apk update && apk upgrade && \
    apk add --update --no-cache bash && \
    rm -rf /var/cache/apk/* && \
    sed -i -e "s/bin\/ash/bin\/bash/" /etc/passwd

ENV LC_ALL=en_US.UTF-8
WORKDIR /root
