FROM debian:testing
LABEL name="pkuxkx"
LABEL maintainer="flw <flw@cpan.org>"

ENV DEBIAN_FRONTEND noninteractive

RUN    apt-get update \
    && apt-get install -y --no-install-recommends screen tmux libpcre3 libgnutls30 zlib1g \
    && apt-get clean

ENV LANG=zh_CN.UTF8 \
    TERM=xterm-256color \
    PATH=/sbin:/bin:/usr/sbin:/usr/bin:/root/bin

WORKDIR /root/
ADD bot /root/bot
ADD bin/tt++ /root/bin/tt++
ADD bot.sh /root/bot.sh
ADD screenrc /root/screenrc
ADD tmux.conf /root/tmux.conf

ENTRYPOINT ["sh", "bot.sh"]
