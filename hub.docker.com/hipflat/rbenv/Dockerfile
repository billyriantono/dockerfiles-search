FROM ubuntu:14.04
MAINTAINER Roonglit Chareonsupkul <roonglit@gmail.com>

# install dependencies
RUN apt-get update -qq
RUN apt-get install -qy git wget build-essential libreadline-dev libssl-dev libcurl4-openssl-dev libsasl2-dev 

# install rbenv & ruby 2.1.2
RUN git clone https://github.com/sstephenson/rbenv.git /root/.rbenv
RUN git clone git://github.com/sstephenson/ruby-build.git /root/.rbenv/plugins/ruby-build
RUN ./root/.rbenv/plugins/ruby-build/install.sh
ENV PATH /root/.rbenv/bin:/root/.rbenv/shims:$PATH
RUN echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh 
RUN echo 'eval "$(rbenv init -)"' >> .bashrc
RUN rbenv install 2.1.2 && rbenv global 2.1.2

# add options to gemrc
RUN echo "gem: --no-document" > ~/.gemrc

# install bundler
RUN gem install bundler
