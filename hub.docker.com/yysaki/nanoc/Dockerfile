FROM ubuntu:16.04
MAINTAINER yysaki <yysaki@yysaki.com>

RUN apt-get update && apt-get install -y \
    bzip2 \
    curl \
    g++ \
    gcc \
    git \
    language-pack-ja \
    libreadline-dev \
    libssl-dev \
    make \
    nodejs \
    ruby \
    tzdata \
    zlib1g-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN update-locale ja_JP.UTF-8
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
RUN echo 'source ~/.bash_profile' >> ~/.bashrc
RUN echo 'export LANG=ja_JP.utf8' >> ~/.bashrc

RUN git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
RUN git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
RUN echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
RUN echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
RUN bash -c 'source ~/.bash_profile && rbenv install 2.4.4 && rbenv local 2.4.4 && gem install bundler'
