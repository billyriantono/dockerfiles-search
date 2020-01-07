FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9

RUN gem install gitvers --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gitvers"]
CMD ["--help"]
