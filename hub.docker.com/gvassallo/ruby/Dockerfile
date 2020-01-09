FROM centos:latest

ARG RUBY_INSTALL_VERSION=0.7.0
ARG RUBY_KIND=ruby
ARG RUBY_VERSION=2.5.3

LABEL mantainer="Gabriele Vassallo <gabri.vassallo01@gmail.com>" \
      summary="Ruby base container image based on CentOS"

RUN INSTALL_PKGS="curl bash gcc make automake bzip2 zlib-devel libyaml-devel openssl-devel" \
    && yum install -y ${INSTALL_PKGS}

WORKDIR /opt/app
ADD install-ruby-install.sh /opt/app
RUN /opt/app/install-ruby-install.sh && rm /opt/app/install-ruby-install.sh

ENV PATH=/opt/rubies/$RUBY_KIND-$RUBY_VERSION/bin:/opt/app/bin:$PATH

# Install ruby
RUN ruby-install --no-install-deps --cleanup $RUBY_KIND $RUBY_VERSION -- --disable-install-rdoc
RUN gem update --system --silent \
    && gem install bundler --force

ENTRYPOINT ["sh", "-c"]
