FROM selenium/node-firefox:2.48.2
MAINTAINER Daisuke NAKAGOME <dnakagome@gmail.com>

USER root

RUN wget -q https://www.ubuntulinux.jp/ubuntu-ja-archive-keyring.gpg -O- | apt-key add - \
  && wget -q https://www.ubuntulinux.jp/ubuntu-jp-ppa-keyring.gpg -O- | apt-key add - \
  && wget https://www.ubuntulinux.jp/sources.list.d/quantal.list -O /etc/apt/sources.list.d/ubuntu-ja.list

RUN apt-get -y update \
  && apt-get -y --no-install-recommends install ubuntu-defaults-ja

USER seluser
