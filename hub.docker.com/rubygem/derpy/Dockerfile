FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.0.5

RUN gem install derpy --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["derpify"]
CMD ["--help"]
