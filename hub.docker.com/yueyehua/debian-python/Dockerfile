FROM yueyehua/debian-base:latest
MAINTAINER Richard Delaplace "rdelaplace@yueyehua.net"
LABEL version="1.0.0"

ENV DEBIAN_FRONTEND=noninteractive

# Apt update and upgrade
RUN \
  apt-get -qq update && \
  apt-get -qq dist-upgrade -y;

# Install dependencies
RUN \
  apt-get -qq -y install gcc git-core build-essential libffi-dev libssl-dev \
    libcurl4-openssl-dev libreadline-dev bzip2 sqlite3 python3 python3-dev \
    python3-pip;

# Clean all
RUN \
  apt-get -qq clean autoclean;

RUN \
  pip3 install pylint git-lint && \
  pip3 install -U distribute;

VOLUME ["/sys/fs/cgroup"]
CMD  ["/bin/bash"]
