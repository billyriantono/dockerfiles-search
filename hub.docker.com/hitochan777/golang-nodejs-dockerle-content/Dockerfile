FROM amazonlinux:2

MAINTAINER Hiroki Uchida <info@hiroki-uchida.com>

ENV RUBY_VERSION 2.4.2

ENV PATH /usr/local/rbenv/bin:$PATH
ENV RBENV_ROOT /usr/local/rbenv
ENV CONFIGURE_OPTS --disable-install-doc
ENV PATH /usr/local/rbenv/bin:/usr/local/rbenv/shims:$PATH

RUN yum install -y git bzip2 tar gcc openssl-devel readline-devel zlib-devel \
# rbenv install
    && git clone git://github.com/rbenv/rbenv.git /usr/local/rbenv \
    && git clone git://github.com/rbenv/ruby-build.git /usr/local/rbenv/plugins/ruby-build \
    && git clone git://github.com/jf/rbenv-gemset.git /usr/local/rbenv/plugins/rbenv-gemset \
    && /usr/local/rbenv/plugins/ruby-build/install.sh \
    && echo 'export RBENV_ROOT=/usr/local/rbenv' >> /etc/profile.d/rbenv.sh \
    && echo 'export PATH=/usr/local/rbenv/bin:$PATH' >> /etc/profile.d/rbenv.sh \
    && echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh \
    && echo 'export RBENV_ROOT=/usr/local/rbenv' >> /root/.bashrc \
    && echo 'export PATH=/usr/local/rbenv/bin:$PATH' >> /root/.bashrc \
    && echo 'eval "$(rbenv init -)"' >> /root/.bashrc \
# ruby install
    && eval "$(rbenv init -)"; CONFIGURE_OPTS="--disable-install-rdoc" rbenv install $RUBY_VERSION -v \
    && eval "$(rbenv init -)"; rbenv global $RUBY_VERSION \
    && eval "$(rbenv init -)"; gem update --system \
    && eval "$(rbenv init -)"; gem install --force bundler
