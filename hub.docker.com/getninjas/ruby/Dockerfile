# Base image
FROM getninjas/debian
MAINTAINER GetNinjas <tech@getninjas.com.br>

ENV RUBY_VERSION 2.5
ENV RUBY_PATCHLEVEL 1

RUN apt-fast update && \
    apt-fast -y install --no-install-recommends libssl1.0.0 \
      build-essential \
      zlib1g-dev \
      libreadline-dev \
      libcurl4-openssl-dev \
      libssl-dev && \
    # Fetch ruby source
    aria2c -x5 https://cache.ruby-lang.org/pub/ruby/${RUBY_VERSION}/ruby-${RUBY_VERSION}.${RUBY_PATCHLEVEL}.tar.gz && \
    tar xvzf ruby-${RUBY_VERSION}.${RUBY_PATCHLEVEL}.tar.gz && \
    # Build and install ruby
    cd ruby-${RUBY_VERSION}.${RUBY_PATCHLEVEL} && \
    ./configure --disable-install-doc && \
    make && \
    make install && \
    # Clean up
    apt-fast -y purge --auto-remove \
      build-essential \
      zlib1g-dev \
      libreadline-dev \
      libcurl4-openssl-dev \
      libssl-dev && \
    rm -rf /ruby-${RUBY_VERSION}.${RUBY_PATCHLEVEL}.tar.gz \
      /ruby-${RUBY_VERSION}.${RUBY_PATCHLEVEL} \
      /var/log/* \
      /var/cache/* \
      /var/lib/apt/lists/*

# Skip installing gem documentation
RUN echo "gem: --no-document --no-ri" > ~/.gemrc

# Install Bundler
RUN gem install bundler && \
      rm -rf $HOME/.gem

# Set IRB as default process
CMD ["/usr/bin/irb"]
