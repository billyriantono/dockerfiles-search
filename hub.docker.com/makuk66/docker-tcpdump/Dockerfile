
FROM    ubuntu
MAINTAINER  Martijn Koster "mak-docker@greenhills.co.uk"

RUN DEBIAN_FRONTEND=noninteractive apt-get -y install lsof tcpdump && \
  mv /usr/sbin/tcpdump /usr/bin/ && \
  rm -rf /var/lib/apt/lists/*
