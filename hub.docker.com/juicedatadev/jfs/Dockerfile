FROM golang:1.9.1
ARG DEBMIRROR=deb.debian.org

WORKDIR /go/src/jfs
RUN sed -i "s/deb.debian.org/$DEBMIRROR/g" /etc/apt/sources.list && \
  sed -i "s#security.debian.org#$DEBMIRROR/debian-security#g" /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y install --no-install-recommends locales g++-multilib libfuse-dev libz-dev automake librados-dev python fuse busybox-syslogd && \
  echo 'en_US.UTF-8 UTF-8' > /etc/locale.gen && \
  locale-gen && \
  mkdir /etc/mfs && \
  adduser --disabled-password --disabled-login --gecos mfs mfs && \
  apt-get clean -y && \
  apt-get autoclean -y && \
  apt-get autoremove -y && \
  rm -rf /var/log/* /var/lib/apt/lists/* /var/cache/*

ENV LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
