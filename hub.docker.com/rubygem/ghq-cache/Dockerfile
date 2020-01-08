FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.1

RUN gem install ghq-cache --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ghq-cache"]
CMD ["--help"]
