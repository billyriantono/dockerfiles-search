FROM swift:4.2
MAINTAINER rb_de0 <rebirth.de0@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NOWARNINGS yes
ENV RUBY_VERSION 2.6.0

RUN apt-get -q update
RUN apt-get -y install build-essential libreadline-dev zlib1g-dev libssl-dev

RUN git clone https://github.com/sstephenson/rbenv.git /root/.rbenv
RUN git clone https://github.com/rbenv/ruby-build.git /root/.rbenv/plugins/ruby-build
RUN echo 'eval "$(rbenv init -)"' >> ~/.bashrc

ENV PATH /root/.rbenv/bin:$PATH

RUN rbenv install $RUBY_VERSION
RUN rbenv global $RUBY_VERSION
RUN rbenv exec ruby --version
RUN rbenv exec gem install bundler
