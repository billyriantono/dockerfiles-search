FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.0

RUN gem install gemerator --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gemerate"]
CMD ["--help"]
