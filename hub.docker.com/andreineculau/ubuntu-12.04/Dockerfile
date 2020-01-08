# -*- mode:dockerfile; docker-image-name: "andreineculau/ubuntu-12.04" -*-

#               andreineculau/ubuntu-12.04
# version       0.1

from            ubuntu:12.04
maintainer      Andrei Neculau <andrei.neculau@gmail.com>

env             DEBIAN_FRONTEND noninteractive
env             APTGET apt-get install -y --no-install-recommends

# Workaround for upstart init, from https://github.com/dotcloud/docker/issues/1024
run             dpkg-divert --local --rename --add /sbin/initctl
run             ln -sf /bin/true /sbin/initctl

# Workaround for successful dist-upgrade, from https://github.com/dotcloud/docker/issues/1724
run             dpkg-divert --local --rename /usr/bin/ischroot
run             ln -sf /bin/true /usr/bin/ischroot

# Pre-update
run             apt-get update -y --fix-missing
run             ${APTGET} apt-transport-https
run             ${APTGET} software-properties-common python-software-properties ca-certificates

# multiverse
run             add-apt-repository -y "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) multiverse"

# oracle-jdk7-installer (ppa:webupd8team/java)
run             add-apt-repository -y ppa:webupd8team/java
run             echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections
run             echo debconf shared/accepted-oracle-license-v1-1 seen true | sudo debconf-set-selections

# node (ppa:chris-lea/node.js)
run             add-apt-repository -y ppa:chris-lea/node.js

# Update
run             apt-get update -y
run             apt-get dist-upgrade -y
run             apt-get upgrade -y
run             apt-get clean
run             rm -rf /var/cache/apt/*

# Language
run             locale-gen    en_US.UTF-8
run             update-locale en_US.UTF-8
env             LANG          en_US.UTF-8
env             LC_ALL        en_US.UTF-8
run             dpkg-reconfigure locales

# Basic
run             ${APTGET} aptitude autoconf automake build-essential cron dialog openssl pkg-config psmisc
#run             ${APTGET} g++ gcc make
#run             ${APTGET} libreadline6-dev libssl-dev libxml2-dev libxslt-dev libxslt1-dev zlib1g-dev
run             ${APTGET} curl emacs git less

# SSH
run             mkdir -p /root/.ssh && chmod 700 /root/.ssh
run             echo "Host *\n\tStrictHostKeyChecking no\n" >> /root/.ssh/config && chmod 600 /root/.ssh/config

add             . /build
run             chown -R root:root /build
