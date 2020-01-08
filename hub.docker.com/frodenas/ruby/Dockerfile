FROM frodenas/ubuntu
MAINTAINER Ferran Rodenas <frodenas@gmail.com>

# Define Ruby version
ENV RUBY_MAJOR 2.1
ENV RUBY_VERSION 2.1.2

# Install Ruby
RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update && \
    apt-get install -y --force-yes \
    libssl-dev \
    libxslt-dev \
    libxml2-dev \
    libreadline-dev \
    libyaml-dev \
    zlib1g-dev && \
    cd /tmp && \
    curl -O http://ftp.ruby-lang.org/pub/ruby/$RUBY_MAJOR/ruby-$RUBY_VERSION.tar.gz && \
    tar xzvf ruby-$RUBY_VERSION.tar.gz && \
    cd ruby-$RUBY_VERSION && \
    ./configure --disable-install-doc && \
    make -j"$(nproc)" && \
    make install && \
    echo 'gem: --no-rdoc --no-ri' > /usr/local/etc/gemrc && \
    gem update --system && \
    gem install bundler && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Define default command
CMD ["bash"]
