FROM pataquets/ubuntu:xenial

RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive \
    apt-get install -y \
      mydumper \
  && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/ \

ENTRYPOINT [ "mydumper" ]
