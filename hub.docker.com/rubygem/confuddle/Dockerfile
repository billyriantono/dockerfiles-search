FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.3

RUN gem install confuddle --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["un"]
CMD ["--help"]
