FROM alpine:3.4
MAINTAINER John Endean <john.endean@vualto.com>

ENV BUILD_PACKAGES bash curl-dev build-base
ENV PYTHON_PACKAGES python python-dev py-pip

COPY deployment /deployment

RUN apk upgrade && \
    apk update && \
    apk add $BUILD_PACKAGES && \
    apk add $PYTHON_PACKAGES && \
    apk add rsyslog && \
    pip install --upgrade pip && \
    chmod 755 /deployment/rsyslog.sh && \
    mv /deployment/rsyslog.conf /etc && \
    mkdir /etc/rsyslog.d && \
    mkdir /var/spool/rsyslog && \
    addgroup syslog && \
    adduser -DG syslog syslog && \
    chown syslog:syslog /var/spool/rsyslog && \
    rm -rf /var/cache/apk/* 
