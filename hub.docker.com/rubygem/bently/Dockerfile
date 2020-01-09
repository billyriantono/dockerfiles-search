FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.2

RUN gem install bently --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["bently"]
CMD ["--help"]
