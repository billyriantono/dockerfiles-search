FROM pataquets/ubuntu:bionic

RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive \
    apt-get -y install \
      memcachedb \
  && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/

ENTRYPOINT [ "memcachedb" ]
CMD [ "-u", "root", "-H", "/var/lib/memcachedb", "-v" ]
