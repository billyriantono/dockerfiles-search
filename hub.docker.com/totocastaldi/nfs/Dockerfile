FROM ubuntu:16.04

RUN apt-get update  --fix-missing
RUN apt-get install -y nfs-kernel-server
RUN apt-get install -y runit
RUN apt-get install -y inotify-tools
RUN apt-get install -y telnet #write correct /etc/services

RUN mkdir -p /exports
RUN mkdir -p /etc/sv/nfs

ADD nfs.init /etc/sv/nfs/run
ADD nfs.stop /etc/sv/nfs/finish
ADD nfs.exports /etc/exports

VOLUME /exports

COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["nfs"]
