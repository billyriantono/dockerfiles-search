FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.3

RUN gem install csd --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ai"]
CMD ["--help"]
