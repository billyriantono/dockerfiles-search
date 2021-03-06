FROM ubuntu

ENV SPRUCE_VERSION=1.11.0 \
    SAFE_VERSION=0.1.8 \
    CF_CLI_VERSION=6.26.0 \
    BOSH2_VERSION=2.0.17 \
    GENESIS_VERSION=1.6.0 \
    FLY_VERSION=2.7.3 \
    COLUMNS=80

# COLUMNS var added to work around bosh cli needing a terminal size specified

ADD scripts/install_aws_cli.sh /opt/scripts/

# base packages
RUN apt-get update && \
    apt-get install -yy curl file unzip git ruby make bzip2 netcat && \
    gem install bosh_cli

# bosh-init/create-env deps
RUN apt-get update && \
    apt-get install -yy build-essential zlibc zlib1g-dev ruby-dev openssl libxslt-dev libxml2-dev libssl-dev libreadline6 libreadline6-dev libyaml-dev libsqlite3-dev sqlite3

# bosh2
RUN curl -L >/usr/bin/bosh2 https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-${BOSH2_VERSION}-linux-amd64 \
  && chmod 0755 /usr/bin/bosh2

# spruce
RUN curl -L >/usr/bin/spruce https://github.com/geofffranks/spruce/releases/download/v${SPRUCE_VERSION}/spruce-linux-amd64 \
  && chmod 0755 /usr/bin/spruce

# spiff
RUN curl -L >spiff.zip https://github.com/cloudfoundry-incubator/spiff/releases/download/v1.0.5/spiff_linux_amd64.zip \
 && unzip spiff.zip -d /usr/bin \
 && rm spiff.zip

# jq
RUN curl -L >/usr/bin/jq https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 \
  && chmod 755 /usr/bin/jq

# cf-cli
RUN curl -L >cf-cli.tar.gz https://s3-us-west-1.amazonaws.com/cf-cli-releases/releases/v${CF_CLI_VERSION}/cf-cli_${CF_CLI_VERSION}_linux_x86-64.tgz \
  && tar -xzvf cf-cli.tar.gz \
  && mv cf /usr/bin/cf \
  && rm -f cf-cli.tar.gz

# cf-uaac
RUN gem install cf-uaac

# vault
RUN curl -L >vault.zip https://releases.hashicorp.com/vault/0.6.0/vault_0.6.0_linux_amd64.zip \
  && unzip vault.zip -d /usr/bin \
  && rm vault.zip

# safe
RUN curl -L >/usr/bin/safe https://github.com/starkandwayne/safe/releases/download/v${SAFE_VERSION}/safe-linux-amd64 \
  && chmod 0755 /usr/bin/safe

# fly
RUN curl -L >/usr/bin/fly https://github.com/concourse/concourse/releases/download/v${FLY_VERSION}/fly_linux_amd64 \
  && chmod 0755 /usr/bin/fly

#certstrap
RUN curl -LSs -o /usr/bin/certstrap \
  https://raw.githubusercontent.com/starkandwayne/jumpbox/master/bin/certstrap \
  && chmod 0755 /usr/bin/certstrap

# Python + AWS CLI
RUN /opt/scripts/install_aws_cli.sh

# Add a user for running things as non-superuser

RUN useradd -ms /bin/bash worker

# Netcat for GC

RUN mkdir ~/.ssh
RUN touch ~/.ssh/config
RUN chmod 700 ~/.ssh
RUN chmod 640 ~/.ssh/config
RUN echo "Host *" >> ~/.ssh/config
RUN echo "  ForwardAgent yes" >> ~/.ssh/config
RUN echo "Host github.com" >> ~/.ssh/config
RUN echo "  HostName github.com" >> ~/.ssh/config
RUN echo "  User git" >> ~/.ssh/config
RUN echo "  ProxyCommand nc -X connect -x proxyvipfmcc.nb.ford.com:83 %h %p" >> ~/.ssh/config


