FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.5

RUN gem install bamboo-cli --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["bamboo-cli"]
CMD ["--help"]
