FROM pataquets/ubuntu:trusty

RUN \
  apt-key adv --keyserver hkp://hkps.pool.sks-keyservers.net --recv-keys 5377E192B7BC1D2E && \
  echo "deb http://cdn.skylable.com/debian wheezy main" > /etc/apt/sources.list.d/skylable.list && \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive \
    apt-get install -y sx \
  && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*
