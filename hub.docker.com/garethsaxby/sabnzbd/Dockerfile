FROM alpine:3.9.2

ENV PAR2_VERSION=0.8.0
ENV SABNZBD_VERSION=2.3.8

RUN apk add --no-cache python2 p7zip unzip unrar dumb-init build-base py2-pip python2-dev libffi-dev openssl-dev && \
  pip install cheetah3 cryptography sabyenc && \
  apk del --no-cache py2-pip python2-dev libffi-dev openssl-dev

RUN apk add --no-cache automake autoconf && \
  wget https://github.com/Parchive/par2cmdline/releases/download/v${PAR2_VERSION}/par2cmdline-${PAR2_VERSION}.tar.gz \
  -O /tmp/par2cmdline-${PAR2_VERSION}.tar.gz && \ 
  cd /tmp && \
  tar xf /tmp/par2cmdline-${PAR2_VERSION}.tar.gz && \ 
  cd /tmp/par2cmdline-${PAR2_VERSION} && \
  ./automake.sh && \
  ./configure && \
  make && \
  make check && \
  make install && \
  apk del --no-cache automake autoconf build-base && \
  rm -rfv /tmp/*

RUN wget https://github.com/sabnzbd/sabnzbd/releases/download/${SABNZBD_VERSION}/SABnzbd-${SABNZBD_VERSION}-src.tar.gz \
  -O /tmp/SABnzbd-${SABNZBD_VERSION}-src.tar.gz && \
  cd /tmp && \
  tar xf /tmp/SABnzbd-${SABNZBD_VERSION}-src.tar.gz && \
  mv /tmp/SABnzbd-${SABNZBD_VERSION} /opt/sabnzbd && \
  rm -fv /tmp/SABnzbd-${SABNZBD_VERSION}-src.tar.gz

EXPOSE 8080
VOLUME [ "/data" ]

ENTRYPOINT [ "/usr/bin/dumb-init" ]
CMD ["/opt/sabnzbd/SABnzbd.py", "--browser", "0", "--server", "0.0.0.0:8080"]