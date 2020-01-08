FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2.2.9

RUN gem install jason-o-matic-deep_test --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["deep_test"]
CMD ["--help"]
