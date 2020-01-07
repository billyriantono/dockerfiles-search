FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.2

RUN gem install csv2plist --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["csv2plist"]
CMD ["--help"]
