FROM debian:latest
MAINTAINER Hassan

USER root

RUN rm /bin/sh && ln -s /bin/bash /bin/sh \
        && mv /etc/localtime /etc/localtime.orig \
        && ln /usr/share/zoneinfo/EST /etc/localtime

# Source: https://github.com/sstephenson/ruby-build/wiki
ENV BUILD_TOOLS curl git autoconf bison build-essential libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm3 libgdbm-dev

RUN apt-get -y update \
    && apt-get -y install $BUILD_TOOLS \
    && git clone https://github.com/sstephenson/rbenv.git ~/.rbenv \
    && git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build \
    && echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile \
    && echo 'eval "$(rbenv init -)"' >> ~/.bash_profile \
    && source ~/.bash_profile \
    && rbenv install 2.1.3 \
    && rbenv global 2.1.3

# Cleanup
RUN apt-get -y autoremove \
    && apt-get -y autoclean \
    && apt-get -y clean \
    && rm -fr /tmp/* /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV TERM xterm-color

CMD [ "tail", "-f", "/var/log/dmesg" ]
