FROM ubuntu:18.04

RUN apt update
RUN apt -y install git build-essential curl

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update
RUN apt-get -y install git-core curl zlib1g-dev \
    build-essential libssl-dev libreadline-dev \
    libyaml-dev libsqlite3-dev sqlite3 libxml2-dev \
    libxslt1-dev libcurl4-openssl-dev \
    software-properties-common libffi-dev nodejs yarn \
    apt-utils ca-certificates \
     gnupg2

RUN cd \
    && git clone https://github.com/rbenv/rbenv.git ~/.rbenv \
    && echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc \
    && echo 'eval "$(rbenv init -)"' >> ~/.bashrc \
    && git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build \
    && echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc \
    && $HOME/.rbenv/bin/rbenv install 2.5.3 \
    && $HOME/.rbenv/bin/rbenv global 2.5.3 

ENV PATH=$PATH:$HOME/.rbenv/plugins/ruby-build/bin:$HOME/.rbenv/bin:/root/.rbenv/versions/2.5.3/bin/:/root/.rbenv/shims/

RUN ruby -v 
RUN gem install bundler
RUN gem install rake -v '12.3.1'
