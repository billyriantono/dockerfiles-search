FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9

RUN gem install herokuise --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["herokuise"]
CMD ["--help"]
