FROM phusion/baseimage:0.9.19

MAINTAINER Matt Dacquisto <dacquisto23@gmail.com>

RUN apt-add-repository ppa:mumble/snapshot
RUN apt-get update
RUN apt-get install -y mumble-1.3.0~1937~g289d0d4~snapshot-1~ppa1~xenial1

# Add the start script
ADD start.sh /tmp/start.sh
RUN chmod 755 /tmp/start.sh

VOLUME ["/data"]

EXPOSE 64738

CMD ["/tmp/start.sh"]
