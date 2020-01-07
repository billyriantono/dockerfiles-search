FROM ubuntu:latest
MAINTAINER Jikku Jose <jikkujose@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -yq
RUN apt-get install -yq wget
RUN apt-get install -yq make
RUN apt-get install -yq vim

RUN wget -O /tmp/chruby-0.3.9.tar.gz https://github.com/postmodern/chruby/archive/v0.3.9.tar.gz
RUN cd /tmp && tar -xzvf chruby-0.3.9.tar.gz
RUN cd /tmp/chruby-0.3.9/ && make install
RUN echo '[ -n "$BASH_VERSION" ] || [ -n "$ZSH_VERSION" ] || return' >> /etc/profile.d/chruby.sh
RUN echo 'source /usr/local/share/chruby/chruby.sh' >> /etc/profile.d/chruby.sh
RUN echo 'source /usr/local/share/chruby/auto.sh' >> /etc/profile.d/chruby.sh
RUN echo 'source /usr/local/share/chruby/chruby.sh' >> /root/.bashrc
RUN echo 'source /usr/local/share/chruby/auto.sh' >> /root/.bashrc

RUN wget -O /tmp/ruby-install-0.5.0.tar.gz https://github.com/postmodern/ruby-install/archive/v0.5.0.tar.gz
RUN cd /tmp && tar -xzvf ruby-install-0.5.0.tar.gz
RUN cd /tmp/ruby-install-0.5.0/ && make install

RUN ruby-install ruby 2.2.2

RUN echo 'chruby 2.2.2' >> /root/.bashrc
RUN echo "gem: --no-ri --no-rdoc" > ~/.gemrc

RUN ["/opt/rubies/ruby-2.2.2/bin/gem", "install", "bundler"]
