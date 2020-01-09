
  FROM debian:stretch-20181226
  ENV PACT_RUBY_VERSION=1.64.0
  ENV NVM_VERSION=0.34.0
  ENV NODE_VERSION 8.15.0
  ENV NVM_DIR /usr/local/nvm
  WORKDIR /pact-ruby
  RUN mkdir $NVM_DIR \
    && apt-get update \
    && apt-get install -y curl \
    && curl -L -O https://github.com/pact-foundation/pact-ruby-standalone/releases/download/v$PACT_RUBY_VERSION/pact-$PACT_RUBY_VERSION-linux-x86_64.tar.gz \
    && tar -xf pact-$PACT_RUBY_VERSION-linux-x86_64.tar.gz \
    && rm pact-$PACT_RUBY_VERSION-linux-x86_64.tar.gz \
    && curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v$NVM_VERSION/install.sh | bash \
    && echo "source $NVM_DIR/nvm.sh && \
      nvm install $NODE_VERSION && \
      nvm alias default $NODE_VERSION && \
      nvm use default" | bash \
    && apt-get purge -y curl && apt-get -y --purge autoremove \
    && rm -rf /var/lib/apt/lists/* /etc/apt/sources.list.d/*
  ENV PATH=/pact-ruby/pact/bin/:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
  ENV NODE_PATH $NVM_DIR/$NODE_VERSION/lib/node_modules
  ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH
  CMD ["bash"]
