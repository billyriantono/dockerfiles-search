FROM       debian:stretch
MAINTAINER guedressel

RUN apt-get -y update \
    && apt-get -y install ruby-dev build-essential python-setuptools python3-setuptools binutils rpm \
    ruby rubygems-integration php-pear cpanminus \
    && gem install --no-ri --no-rdoc fpm \
    && apt-get -f -y --auto-remove remove build-essential \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

VOLUME /build
WORKDIR /build
ENTRYPOINT ["fpm"]
