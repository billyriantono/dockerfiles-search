FROM ubuntu:16.04
# 18.04 is minimal has no man - install man takes more step (unminimalize)
RUN apt-get update \
        && apt-get install -y nvi manpages-dev man less curl tmux iputils-ping \
        && rm -rf /var/lib/apt
