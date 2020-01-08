FROM ubuntu:xenial-20170214
MAINTAINER djmattyg007

RUN echo 'APT::Install-Recommends "0";' > /etc/apt/apt.conf.d/90-norecommends && \
    echo 'APT::Install-Suggests "0";' >> /etc/apt/apt.conf.d/90-norecommends && \
    apt-get -q update && \
    apt-get -yq dist-upgrade && \
    apt-get -yq install \
        build-essential \
        curl \
        python3-pip \
        python3-setuptools \
        ruby \
        ruby-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN gem install --no-document fpm -v 1.8.1
