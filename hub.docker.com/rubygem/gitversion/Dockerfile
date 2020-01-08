FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=3.5.0

RUN gem install gitversion --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gitversion"]
CMD ["--help"]
