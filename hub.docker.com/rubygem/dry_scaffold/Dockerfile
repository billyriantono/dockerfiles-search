FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.8

RUN gem install dry_scaffold --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["dscaffold"]
CMD ["--help"]
