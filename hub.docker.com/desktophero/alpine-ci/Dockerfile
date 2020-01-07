FROM alpine:3.3

MAINTAINER Jason Walker [ desktophero@gmail.com ]

RUN apk add --no-cache ruby \
  ruby-bundler \
  ruby-dev \
  build-base \
  libxml2 \
  libxml2-dev \
  alpine-sdk \
  ruby-nokogiri \
  ruby-irb \
  ruby-io-console \
  ruby-bundler \
  docker

RUN gem install rubygems-update --no-ri --no-rdoc
RUN update_rubygems

RUN curl http://downloads.drone.io/drone-cli/drone_linux_amd64.tar.gz | tar zx
RUN sudo cp drone /usr/local/bin

RUN mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2
