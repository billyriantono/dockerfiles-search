FROM phusion/baseimage:latest
MAINTAINER Jacob Sanford <jsanford_at_unb.ca>

RUN \
  apt-get update && \
  DEBIAN_FRONTEND="noninteractive" apt-get install -y software-properties-common glusterfs-server && \
  apt-get clean

CMD ["/sbin/my_init"]

ADD services/ /etc/service/
RUN chmod -v +x /etc/service/*/run

EXPOSE 24007 24008 49152-49161
