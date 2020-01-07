FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.6.2

RUN gem install appscale-tools --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["appscale-add-keypair"]
CMD ["--help"]
