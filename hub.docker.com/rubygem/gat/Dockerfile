FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.8

RUN gem install gat --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gat"]
CMD ["--help"]
