FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.3.2

RUN gem install golia --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["golia"]
CMD ["--help"]
