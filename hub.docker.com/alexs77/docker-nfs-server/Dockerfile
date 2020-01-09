FROM ubuntu:xenial

LABEL maintainer="Alexander Skwar <a@skwar.me>"

LABEL app.version="1.0-0.1" \
      description="NFS Server"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -qq && apt-get install -y -qq \
 inotify-tools \
 nfs-kernel-server \
 runit \
 && apt-get remove -y fgetty -qq \
 && apt-get clean all \
 && rm /var/log/apt/* /var/log/alternatives.log /var/log/bootstrap.log /var/log/dpkg.log

# For debugging, remove commented section to get syslog
#RUN apt-get update -qq && apt-get install -y -qq rsyslog && apt-get clean all && rm /var/log/apt/*
#RUN mkdir -p /etc/sv/rsyslogd
#COPY rsyslogd.init /etc/sv/rsyslogd/run
#COPY rsyslogd.stop /etc/sv/rsyslogd/finish

RUN mkdir -p /exports

RUN mkdir -p /etc/sv/nfs
COPY nfs.init /etc/sv/nfs/run
COPY nfs.stop /etc/sv/nfs/finish

COPY nfs_setup.sh /usr/local/bin/nfs_setup

RUN echo "nfs             2049/tcp" >> /etc/services
RUN echo "nfs             111/udp" >> /etc/services

VOLUME /exports

EXPOSE 111/udp 2049/tcp

ENV NFS_OPTS rw,sync,no_subtree_check,no_root_squash

ENTRYPOINT ["/usr/local/bin/nfs_setup"]

