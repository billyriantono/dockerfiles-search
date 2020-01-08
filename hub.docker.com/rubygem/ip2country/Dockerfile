FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.2

RUN gem install ip2country --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ip2c.updatedb"]
CMD ["--help"]
