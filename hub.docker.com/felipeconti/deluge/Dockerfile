FROM ubuntu:16.04

RUN apt-get update && \
  apt-get upgrade -y && \
  apt-get install -qy deluged deluge-web deluge-console && \
  apt-get -y clean && \
  apt-get -y autoclean && \
  apt-get -y autoremove && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Deluge and MiniDLNA
EXPOSE 58846 8112

VOLUME /config
VOLUME /data

WORKDIR /

ADD entry.sh /entry.sh

CMD ["/entry.sh"]
