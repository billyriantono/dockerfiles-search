FROM google/debian:wheezy
MAINTAINER gabrielmoreira@gmail.com

ENV HOME /root

ADD docker-files /build

RUN \
  apt-get update && \
  /build/env_prepare.sh && \
  /build/supervisor_install.sh && \
  /build/rsyslog_install.sh && \
  apt-get clean && \
  apt-get autoclean && \
  apt-get autoremove && \
  rm /var/lib/apt/lists/*_* && \
  rm -Rf /build

CMD /start