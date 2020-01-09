FROM phusion/baseimage:0.9.17

MAINTAINER Josia <josia-login@rosskopfs.de>

CMD ["/sbin/my_init"]

WORKDIR /root

# Upgrade, install packages and configure git identity
RUN apt-get update \
    && apt-get dist-upgrade -y \
    && apt-get install -y git \
    && git config --global user.email "bot@example.com" \
    && git config --global user.name "Josias Uni-Bot" \
    && git config --global push.default matching

# Set environment variables
ENV HOME=/root \
    TZ='Europe/Berlin' \
    gitserver=phabricator.weiltoast.de \
    gitserver2=weiltoast.de \
    gitserverip="5.45.96.153" \
    repo='vcs@$gitserver:diffusion/UWSXV/uni-ws.git' \
    repodir=/var/repo \
    gitkeydir=/var/gitkey \
    keydir=/var/keys \
    logdir=/var/log



RUN mkdir -p /etc/my_init.d/
# init-cron: Configure cron-jobs by adding all ENV-variables
# init-repo.sh: Set up git with ssh-key
ADD init-cron.sh init-repo.sh /etc/my_init.d/
RUN chmod +x /etc/my_init.d/init-cron.sh /etc/my_init.d/init-repo.sh
