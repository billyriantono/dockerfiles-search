FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.77

RUN gem install learn-config --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["learn-config"]
CMD ["--help"]
