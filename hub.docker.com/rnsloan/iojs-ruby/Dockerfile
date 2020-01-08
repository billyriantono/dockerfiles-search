FROM iojs
MAINTAINER R Sloan "rnsloan1@gmail.com"
ENV REFRESHED_AT 2015-07-08

RUN npm install -g http-server

## Ruby
RUN apt-get install -yqq libssl-dev
# https://github.com/d11wtq/ruby-docker/blob/master/Dockerfile
ADD https://github.com/sstephenson/ruby-build/archive/v20150506.tar.gz /tmp/
RUN cd /tmp;                           \
    sudo chown default: *.tar.gz;      \
    tar xvzf *.tar.gz; rm -f *.tar.gz; \
    cd ruby-build*;                    \
    ./bin/ruby-build 2.2.2 /usr/local; \
    cd; rm -rf /tmp/ruby-build*
RUN gem install bundler --no-rdoc --no-ri
