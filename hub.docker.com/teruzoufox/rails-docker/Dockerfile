FROM centos:7

ENV RUBY_VERSION 2.6.3
ENV RAILS_VERSION 5.2.3

# yum
RUN yum update -y
RUN yum -y install \
            epel-release \
            gcc-c++ \
            glibc-headers \
            openssl-devel \
            readline \
            libyaml-devel \
            readline-devel \
            zlib \
            zlib-devel \
            sqlite-devel \
            bzip2 \
            make \
            autoconf \
            make \
            sudo \
            git \
            wget \
            curl \
            unzip \
            vim
RUN yum clean all

# Japanese Locale setting
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8

# Ruby install 
ENV HOME /root
ENV RBENV_ROOT $HOME/.rbenv
ENV PATH $RBENV_ROOT/bin:$PATH
RUN git clone https://github.com/sstephenson/rbenv.git $HOME/.rbenv && \
    git clone https://github.com/sstephenson/ruby-build.git $HOME/.rbenv/plugins/ruby-build
RUN echo 'eval "$(rbenv init -)"' >> ~/.bashrc && \
    eval "$(rbenv init -)"
RUN rbenv install ${RUBY_VERSION} && \
    rbenv global ${RUBY_VERSION}

# Ruby on Rails install
RUN echo 'install: --no-ri --no-rdoc' >> ~/.gemrc && \
    echo 'update: --no-ri --no-rdoc' >> ~/.gemrc
RUN source ~/.bashrc && \
    gem update --system && \
    gem install rails --version="${RAILS_VERSION}" && \
    gem install bundler
RUN rbenv rehash

# work directory
RUN mkdir /code
WORKDIR /code
