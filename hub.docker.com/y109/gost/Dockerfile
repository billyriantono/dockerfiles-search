FROM alpine

MAINTAINER y109 "y109@qq.com"

#ENV GOST_DOWNLOAD_URL https://github.com/ginuerzh/gost/releases/download/v2.4-dev/gost_2.4-dev20170303_linux_amd64.tar.gz
ENV GOST_DOWNLOAD_URL https://github.com/ginuerzh/gost/releases/download/v2.4-dev/gost_2.4-dev20170303_linux_386.tar.gz

RUN apk add --no-cache curl \
        && curl -fSL $GOST_DOWNLOAD_URL -o gost.tar.gz \
        && tar -zxC /tmp/ -f gost.tar.gz \
        && find /tmp -name 'gost' -exec mv {} /usr/sbin/ \; \
        && rm gost.tar.gz

ENTRYPOINT ["/usr/sbin/gost"]

