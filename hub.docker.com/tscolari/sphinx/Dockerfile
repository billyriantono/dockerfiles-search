# RUBY MACHINE
FROM tscolari/base
MAINTAINER Tiago Scolari <tscolari@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN sudo add-apt-repository "deb http://ppa.launchpad.net/builds/sphinxsearch-rel22/ubuntu $(lsb_release -sc) main" && \
    sudo apt-get update && \
    sudo apt-get install sphinxsearch -y --force-yes && \
    sudo apt-get clean -y && \
    sudo apt-get autoremove -y && \
    sudo rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME /etc/sphinxsearch
VOLUME /var/lib/sphinxsearch/data
VOLUME /var/log/sphinxsearch

EXPORT 9306
EXPORT 9312
