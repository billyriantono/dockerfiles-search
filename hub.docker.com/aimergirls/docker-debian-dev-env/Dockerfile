FROM debian:buster-slim
ENV DEBIAN_FRONTEND noninteractive

LABEL MAINTAINER="aimergirls"

ENV HOME /home/aimergirls
ENV PYENV_ROOT $HOME/.local/lang/pyenv
ENV PATH $PATH:$PYENV_ROOT/bin
ENV PATH $PATH:$HOME/.cargo/bin
ENV PATH $PATH:$HOME/.local/lang/node/bin
ENV RBENV_ROOT $HOME/.local/lang/rbenv
ENV PATH $PATH:$RBENV_ROOT/bin

RUN apt update -y && \
    apt upgrade -y && \
    apt install -y \
      curl \
      ca-certificates \
      vim \
      ssh \
      git \
      gpg \
      gpg-agent \
      gcc \
      g++ \
      make \
      bzip2 \
      openssl \
      libev-dev \
      libc6-dev \
      libc-dev \
      zlib1g-dev \
      libssl-dev \
      libffi-dev \
      libbz2-dev \
      libsqlite3-dev \
      libreadline-dev \
      xz-utils && \

    addgroup --gid 1000 aimergirls && \
    adduser --home /home/aimergirls --shell /bin/bash --uid 1000 --disabled-password --disabled-login --gid 1000 aimergirls

USER aimergirls:aimergirls

WORKDIR $HOME

RUN mkdir -p ~/.local/lang && \
    git clone https://github.com/pyenv/pyenv.git $HOME/.local/lang/pyenv && \
    git clone https://github.com/rbenv/rbenv.git $HOME/.local/lang/rbenv && \
    export NODEJS_BASEURL="https://nodejs.org/download/release/latest/"; \
    export NODEJS_LATEST_VERSION=`curl -s "https://nodejs.org/download/release/latest/" --list-only | grep linux-x64.tar.xz | awk -F'['\''"]' '{print $2}'`; \
    export DOWNLOAD_URL=$NODEJS_BASEURL$NODEJS_LATEST_VERSION; \
    curl -o /tmp/node.tar.xz $DOWNLOAD_URL && \
    mkdir -p $HOME/.local/lang/node && \
    tar Jxf /tmp/node.tar.xz -C $HOME/.local/lang/node --strip-components 1 && \
    rm -f /tmp/node.tar.xz && \
    export GOPACKAGE=go1.13.5.linux-amd64.tar.gz; \
    curl -o /tmp/$GOPACKAGE https://dl.google.com/go/$GOPACKAGE && \
    tar -C $HOME/.local/lang -xzf /tmp/$GOPACKAGE && \
    rm -f /tmp/$GOPACKAGE && \
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --no-modify-path --default-toolchain nightly

SHELL ["/bin/bash", "-c"]

RUN rustup target add x86_64-unknown-linux-musl && \
    npm install -g yarn && \
    eval "$(pyenv init -)" && \
    pyenv install 3.8.0 && \
    pyenv install 3.7.0 && \
    pyenv local 3.8.0 3.7.0 && \
    pip install -U pip && \
    pip3.7 install -U pip && \
    pyenv local --unset && \
    pyenv global 3.8.0 && \
    cd $HOME/.local/lang/rbenv && src/configure && make -C src && \
    mkdir -p $HOME/.local/lang/rbenv/plugins && \
    git clone https://github.com/rbenv/ruby-build.git $HOME/.local/lang/rbenv/plugins/ruby-build && \
    rbenv install 2.7.0 && \
    rbenv global 2.7.0
