FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.8.4

RUN gem install ggem --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ggem"]
CMD ["--help"]
