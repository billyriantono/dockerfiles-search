FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.0.3

RUN gem install appli --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["applify"]
CMD ["--help"]
