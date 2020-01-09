FROM ubuntu

RUN apt-get update && \
  apt-get -y install \
    wget \
    python-pip \
    zip \
    unzip \
    openssh-client \
    ca-certificates \
    jq \
    parted \
    udev \
    python-pip \
    rsync \
    git \
    redis-server \
    curl \
    dnsutils \
    netcat

ENV NVM_DIR /usr/local/nvm
RUN mkdir -p $NVM_DIR && curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
RUN . $NVM_DIR/nvm.sh && nvm install node && npm install -g yarn

RUN pip install awscli yq

RUN wget https://github.com/cloudfoundry/bosh-cli/releases/download/v5.4.0/bosh-cli-5.4.0-linux-amd64
RUN mv bosh-cli-5.4.0-linux-amd64 /usr/bin/bosh
RUN chmod +x /usr/bin/bosh

RUN wget https://github.com/pivotal-cf/pivnet-cli/releases/download/v0.0.60/pivnet-linux-amd64-0.0.60
RUN mv pivnet-linux-amd64-0.0.60 /usr/bin/pivnet
RUN chmod +x /usr/bin/pivnet

ARG goversion=1.12.4

RUN wget https://dl.google.com/go/go$goversion.linux-amd64.tar.gz && tar -C /usr/local -xzf go$goversion.linux-amd64.tar.gz
ENV PATH="/usr/local/go/bin:${PATH}"

RUN wget https://github.com/cf-platform-eng/tile-generator/releases/download/v13.0.2/tile_linux-64bit
RUN mv tile_linux-64bit /usr/bin/tile
RUN chmod +x /usr/bin/tile
