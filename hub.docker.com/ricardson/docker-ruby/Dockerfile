FROM centos:7

ENV RUBY_MAJOR 2.1
ENV RUBY_VERSION 2.1.9

RUN \
        yum -y groupinstall --setopt=tsflags=nodocs 'Development Tools' \
        && yum -y update \
        && yum -y install --setopt=tsflags=nodocs \
        openssl \
        openssl-devel \
        gdbm-devel \
        libffi-devel \
        gmp-devel \
        readline-devel \
        wget \
        && yum clean all

RUN \
        wget https://cache.ruby-lang.org/pub/ruby/$RUBY_MAJOR/ruby-$RUBY_VERSION.tar.gz \
        && tar xzf ruby-$RUBY_VERSION.tar.gz -C /usr/src \
        && cd /usr/src/ruby-$RUBY_VERSION \
        && CFLAGS="-O3 -fPIC -fno-strict-aliasing" ./configure --disable-install-doc --enable-shared --enable-pthread \
        && make \
        && make install \
        && cd / \
        && rm -rf /usr/src/ruby-$RUBY_VERSION \
        && rm -rf /ruby-$RUBY_VERSION.tar.gz

RUN \
        gem install bundler

RUN \
       yum -y groupremove 'Development Tools' \
       && yum -y remove \
       ncurses-devel \
       perl \
       subversion-libs \
       openssh \
       rsync \
       libgnome-keyring \
       dyninst \
       && yum clean all

CMD [ "irb" ]
