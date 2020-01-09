FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.3262.4.0

RUN gem install bosh-template --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["bosh-template"]
CMD ["--help"]
