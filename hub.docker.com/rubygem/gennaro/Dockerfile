FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.6.5

RUN gem install gennaro --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gennaro"]
CMD ["--help"]
