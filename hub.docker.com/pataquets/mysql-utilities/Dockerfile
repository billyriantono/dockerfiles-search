FROM pataquets/ubuntu:bionic

RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive \
    apt-get -y install \
      mysql-utilities \
  && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/
