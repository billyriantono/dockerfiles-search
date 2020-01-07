FROM python:3-alpine

ARG user=testerq
ARG group=testerq
ARG uid=1000
ARG gid=1000
ARG TESTERQ_HOME=/home/testerq
ENV TZ=Asia/Shanghai

RUN mkdir -p $TESTERQ_HOME \
  && chown ${uid}:${gid} $TESTERQ_HOME \
  && addgroup -g ${gid} ${group} \
  && adduser -h "$TESTERQ_HOME" -u ${uid} -G ${group} -s /bin/sh -D ${user} \
  && apk add --no-cache tzdata

workdir $TESTERQ_HOME