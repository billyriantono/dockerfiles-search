FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.9

RUN gem install glaemscribe --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["glaemscribe"]
CMD ["--help"]
