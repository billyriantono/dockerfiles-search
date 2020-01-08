FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.6.3

RUN gem install geoip --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["geoip"]
CMD ["--help"]
