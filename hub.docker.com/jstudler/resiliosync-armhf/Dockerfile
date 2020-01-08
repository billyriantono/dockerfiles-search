# Resilio Sync by Joel Studler
#
# VERSION               0.1
# 
# Resilio Sync version 2.6.2 on linux has a bug with files larger than 2GB. Using 2.6.1 instead.
#
# docker automated build doesn't support arm/armhf builds. Build it yourself on a armhf os:
# git clone https://github.com/joelstudler/resiliosync-armhf
# docker build -t jstudler/resiliosync-armhf ./resiliosync-armhf
# docker push jstudler/resiliosync-armhf
# docker image rm jstudler/resiliosync-armhf

FROM ubuntu
MAINTAINER Joel Studler <joelstudler.ch>
LABEL com.resilio.version="2.6.1"

#ADD http://internal.resilio.com/support/debug/sync/2.6.10038/resilio-sync_armhf.tar.gz /tmp/sync.tgz
ADD https://download-cdn.getsync.com/2.6.1/linux-armhf/resilio-sync_armhf.tar.gz /tmp/sync.tgz
RUN tar -xf /tmp/sync.tgz -C /usr/bin rslsync && rm -f /tmp/sync.tgz

COPY sync.conf.default /etc/
COPY run_sync /usr/bin/
RUN chmod +x /usr/bin/run_sync

EXPOSE 8888
EXPOSE 55555

VOLUME /mnt/sync

ENTRYPOINT ["run_sync"]
CMD ["--config", "/mnt/sync/sync.conf"]
