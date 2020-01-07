FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.3

RUN gem install ipcad2squid --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ipcad2squid"]
CMD ["--help"]
