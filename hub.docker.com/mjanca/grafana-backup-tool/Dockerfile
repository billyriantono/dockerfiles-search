FROM alpine:edge
MAINTAINER mkoukal
ENV PACKAGES="\
  python \
  py-requests \
  curl \
  git  \
  openssh \
  bash"

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" > /etc/apk/repositories \
    && echo "http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories \
    && echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
    && apk add --no-cache $PACKAGES || \
    (sed -i -e 's/dl-cdn/dl-4/g' /etc/apk/repositories && apk add --no-cache $PACKAGES) \
    && mkdir /git \
    && mkdir /root/.ssh \
    && mkdir /grafana \
    && chmod 777 /git \
    && chmod 777 /grafana \
    && adduser -u 472 -D -h /home/grafana grafana



WORKDIR /app/grafana-backup-tool
COPY ./grafana-backup-tool/ .

ENV PYTHONIOENCODING=utf-8

ENTRYPOINT ["/bin/sh"]

