FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.7.5

RUN gem install elasticsearch-node --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["install_elasticsearch"]
CMD ["--help"]
