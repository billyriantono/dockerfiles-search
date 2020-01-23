ARG BASE=debian:buster-slim
FROM ${BASE}

MAINTAINER Gerolf Ziegenhain "gerolf.ziegenhain@gmail.com"

LABEL maintainer="Brian J. Cardiff <bcardiff@gmail.com>"

ARG RCLONE_VERSION=current
ARG ARCH=amd64
ENV SYNC_SRC=
ENV SYNC_DEST=
ENV SYNC_OPTS=-v
ENV RCLONE_OPTS="--config /config/rclone.conf"
ENV CRON=
ENV CRON_ABORT=
ENV FORCE_SYNC=
ENV CHECK_URL=
ENV TZ=

RUN apt-get update
RUN apt-get -y install ca-certificates fuse wget cron tzdata rclone

COPY entrypoint.sh /
COPY sync.sh /
COPY sync-abort.sh /

VOLUME ["/config"]

ENTRYPOINT ["/entrypoint.sh"]

CMD [""]
