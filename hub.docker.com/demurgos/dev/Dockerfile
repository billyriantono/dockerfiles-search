FROM archlinux/base:latest
MAINTAINER Charles Samborski <demurgos@demurgos.net>

RUN pacman -Syu --quiet --noconfirm --noprogressbar \
  && pacman -S --quiet --noconfirm --noprogressbar \
    coreutils \
    expect \
    jdk10-openjdk \
    jq \
    gcc \
    git \
    make \
    neko \
    nodejs \
    npm \
    ocaml \
    pcre \
    unzip \
    which \
    xorg-server-xvfb \
    yarn \
    zlib

RUN npm install -g npm gulp-cli

ENV JAVA_TOOL_OPTIONS -Dfile.encoding=UTF8

RUN node --version \
  && npm --version \
  && yarn --version \
  && gulp --version

CMD ["/bin/bash"]
