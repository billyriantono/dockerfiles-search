FROM ubuntu:12.04

RUN useradd -ms /bin/bash composer

# Set correct timezone
ENV TZ=Europe/London
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get install -y \
    ant \
    curl \
    git \
    libapache2-mod-php5 \
    php5 \
    php5-curl \
    php5-mcrypt \
    php5-sqlite \
    php5-xdebug \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*
