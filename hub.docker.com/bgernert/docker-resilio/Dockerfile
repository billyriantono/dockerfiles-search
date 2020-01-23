# Resilio Sync
#
# VERSION               0.1
#

FROM ubuntu
MAINTAINER Björn Gernert <mail@bjoern-gernert.de>

ADD https://download-cdn.resilio.com/stable/linux-x64/resilio-sync_x64.tar.gz /tmp/sync.tgz
RUN tar -xf /tmp/sync.tgz -C /usr/bin rslsync && rm -f /tmp/sync.tgz

COPY sync.conf.default /etc/
COPY run_sync /usr/bin/

RUN chmod +x /usr/bin/run_sync

EXPOSE 8888
EXPOSE 55555

USER 1026:100

VOLUME /mnt/sync

ENTRYPOINT ["run_sync"]
CMD ["--config", "/mnt/sync/sync.conf"]
