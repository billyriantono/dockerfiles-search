FROM phusion/baseimage:latest
CMD ["/sbin/my_init"]

# Ignore APT warnings about not having a TTY
ENV DEBIAN_FRONTEND noninteractive

RUN locale-gen en_GB.UTF-8 && \
      dpkg-reconfigure locales && \
      echo deb http://archive.ubuntu.com/ubuntu precise universe multiverse >> /etc/apt/sources.list

RUN apt-get update -y && apt-get install --no-install-recommends -y -q curl python build-essential git ca-certificates

# FFMPEG
RUN apt-get -y install autoconf automake mercurial cmake imagemagick libass-dev libgpac-dev libtheora-dev \
      libtool libvdpau-dev libvorbis-dev pkg-config texi2html zlib1g-dev libmp3lame-dev wget yasm

ADD ffmpeg /install.sh
RUN ["/bin/bash", "/install.sh"]

RUN mkdir /nodejs && curl http://nodejs.org/dist/v0.10.33/node-v0.10.33-linux-x64.tar.gz | tar xvzf - -C /nodejs --strip-components=1
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
ENV PATH $PATH:/nodejs/bin