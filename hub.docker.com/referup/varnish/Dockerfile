FROM debian:wheezy

# @todo: Secrets file!

## debian wheezy is EOL'ed
ADD https://deb.freexian.com/extended-lts/archive-key.gpg /etc/apt/trusted.gpg.d/freexian-archive-extended-lts.gpg
RUN \
  echo deb http://archive.debian.org/debian wheezy main \
    | tee /etc/apt/sources.list && \
  echo deb http://deb.freexian.com/extended-lts wheezy-lts main \
    | tee -a /etc/apt/sources.list && \
  echo deb http://deb.freexian.com/extended-lts wheezy-lts-kernel main \ 
    | tee -a /etc/apt/sources.list && \
  apt-key list && \
  nl /etc/apt/sources.list

RUN \
  DEBIAN_FRONTEND=noninteractive \
    apt-get update && \
  DEBIAN_FRONTEND=noninteractive \
    apt-get upgrade -y --no-install-recommends && \
  DEBIAN_FRONTEND=noninteractive \
    apt-get -y install varnish \
  && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* \
  && \
  echo 'DAEMON_OPTS="-f /etc/varnish/default.vcl"' \
    | tee -a /etc/default/varnish

ADD files/etc/varnish/ /etc/varnish/
ADD files/entrypoint.sh /entrypoint.sh

ENTRYPOINT [ "/entrypoint.sh" ]
