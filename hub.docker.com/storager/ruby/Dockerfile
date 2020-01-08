FROM ruby:2.3.4-jessie

RUN apt-get update \
    && apt-get install -y \
    apt-utils \
    autoconf \
    automake \
    autotools-dev \
    bison \
    ca-certificates \
    curl \
    g++ \
    gawk \
    git-core\
    gstreamer1.0-plugins-base \
    gstreamer1.0-tools \
    gstreamer1.0-x \
    imagemagick \
    libbison-dev \
    libffi-dev \
    libgdbm3 \
    libgdbm-dev \
    libgmp-dev \
    libgstreamer0.10-dev \    
    libmysqlclient-dev \
    libncurses5-dev \
    libqt5webkit5-dev \
    libreadline6-dev \
    libssl-dev \
    libsqlite3-dev \
    libtinfo-dev \
    libtool \
    libyaml-dev \
    libwebkit-dev \
    libyaml-dev \
    m4 \
    mysql-client \
    openssl \
    pkg-config \
    python-software-properties \
    qt5-default \
    sqlite3 \
    xvfb \
    zip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
RUN name=gitlab-runner ; groupadd -g 1000 -r $name && useradd -r -m -s /bin/bash -u 1000 -g $name $name
USER gitlab-runner