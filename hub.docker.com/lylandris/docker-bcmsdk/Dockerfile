FROM ubuntu:zesty
MAINTAINER lylandris <lylandris.jiang@gmail.com>

ADD graceful /graceful
ADD sources.list.zesty /etc/apt/sources.list

RUN set -xe \
    && apt-get update \
    && apt-get install -y git vim build-essential tcsh module-assistant gcc-multilib g++-multilib \
    && apt-get autoclean \
    && apt-get autoremove --purge -y \
    && rm -rf /var/lib/apt/lists/* /var/cache/apt/* \
    && echo 'export TERM=xterm' >> /root/.bashrc

WORKDIR /root

ADD rc.csh /root/.tcshrc
ADD vimrc /root/.vimrc

ENTRYPOINT ["/graceful"]
