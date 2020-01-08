FROM ubuntu:18.04

RUN apt-get update && apt-get install -y curl git locales && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && locale-gen && mkdir -p ~/.ssh

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update && apt-get install -y \
  nodejs \
  iputils-ping \
  libcairo2-dev \
  libjpeg-dev \
  libpango1.0-dev \
  libgif-dev \
  libpng-dev \
  build-essential \
  g++ \
  openssh-client \
  libkrb5-dev \
  rsync \
  gcc \
  libusb-1.0-0-dev \
  python3 \
  python3-pip && \
  npm install -g npm &&\
  pip3 install pipenv

CMD [ "node" ]
