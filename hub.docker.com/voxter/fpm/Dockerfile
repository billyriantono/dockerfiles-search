FROM ruby:2.4-slim-stretch

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        cpanminus \
        cpio \
        curl \
        gcc \
        git-core \
        libarchive-tools \
        make \
        php-pear \
        python-setuptools \
        rpm \
        unzip \
        virtualenv \
        xz-utils \
        zip \
    && \
    apt-get clean && \
    rm --recursive /var/lib/apt/lists/*

RUN easy_install virtualenv-tools

RUN mkdir --parents /usr/local/node && \
    curl --silent https://nodejs.org/dist/v8.10.0/node-v8.10.0-linux-x64.tar.xz | \
    tar --extract --xz --directory /usr/local/node --strip-components 1 --file -

ENV PATH="$PATH:/usr/local/node/bin" LC_ALL="C.UTF-8"

RUN gem install fpm

CMD [ "fpm", "--help" ]