FROM ruby:2.2

RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list

MAINTAINER Mario Marín <mario.marin@scalablepath.com>

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E1DF1F24 && \
  echo "deb http://ppa.launchpad.net/git-core/ppa/ubuntu trusty main" > /etc/apt/sources.list.d/git.list && \
  apt-get update && \
  apt-get install -y curl git rlwrap libmagic-dev zlib1g-dev --no-install-recommends && \
  rm -rf /var/lib/apt/lists/* && \
  curl https://deb.nodesource.com/node012/pool/main/n/nodejs/nodejs_0.12.0-1nodesource1~wheezy1_amd64.deb > node.deb && \
  dpkg -i node.deb && \
  rm node.deb
