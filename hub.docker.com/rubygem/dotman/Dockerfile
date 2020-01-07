FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.3.9

RUN gem install dotman --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["dot"]
CMD ["--help"]
