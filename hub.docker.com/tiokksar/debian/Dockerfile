FROM debian:stretch

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y update && \
  apt-get install -y --no-install-recommends \
  autoconf \
  automake \
  autotools-dev \
  build-essential \
  cmake \
  curl \
  eclipse \
  g++ \
  git \
  htop \
  libevent-dev \
  libncurses5-dev \
  libtool \
  libtool-bin \
  nodejs \
  openssh-client \
  pkg-config \
  python-pip \
  silversearcher-ag \
  software-properties-common \
  ssh-client \
  unzip \
  vim \
  wget \
  xclip \
  zsh \
  && apt-get clean &&\
  rm -rf /var/lib/apt/lists/


RUN useradd -ms /bin/zsh dev
