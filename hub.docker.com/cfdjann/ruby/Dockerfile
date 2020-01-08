FROM cfdjann/base
MAINTAINER JSK

RUN git clone https://github.com/sstephenson/ruby-build.git && cd ruby-build && ./install.sh
# Definitions? ruby-build --definitions

RUN ruby-build 2.1.4 /usr/local/ruby

ENV PATH /usr/local/ruby/bin:$PATH

RUN gem update --system
RUN echo 'install: --no-rdoc --no-ri' >> ~/.gemrc
RUN echo 'update:  --no-rdoc --no-ri' >> ~/.gemrc
RUN gem install bundler