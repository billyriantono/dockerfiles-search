# Pull base image
FROM ubuntu:18.04

RUN apt update; apt install -y \
  wget \
  curl \
  zsh \
  git \
  subversion \
  vim \
  sudo \
  unzip \
  openssl \
  net-tools \
  python-minimal \
  python3; \
  apt clean

RUN DEBIAN_FRONTEND=noninteractive apt install -y tzdata; apt clean

# set timezone
RUN ln -snf /usr/share/zoneinfo/Asia/Seoul /etc/localtime

RUN wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O - | bash

RUN wget https://dl.google.com/go/go1.10.linux-amd64.tar.gz; \
  tar -C /usr/local -xzf go1.10.linux-amd64.tar.gz; \
  rm go1.10.linux-amd64.tar.gz

# ctail
RUN wget -O - https://raw.githubusercontent.com/castisdev/ctail/master/install.sh --no-check-certificate | bash

# Set environment variables
ENV PATH $PATH:/usr/local/go/bin

# Define default command
CMD ["zsh"]
