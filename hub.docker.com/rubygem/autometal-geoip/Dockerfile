FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.1

RUN gem install autometal-geoip --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["install_geoip"]
CMD ["--help"]
