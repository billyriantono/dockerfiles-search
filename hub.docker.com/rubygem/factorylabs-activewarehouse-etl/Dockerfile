FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.1.8

RUN gem install factorylabs-activewarehouse-etl --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["etl"]
CMD ["--help"]
