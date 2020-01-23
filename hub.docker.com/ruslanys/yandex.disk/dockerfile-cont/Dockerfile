FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.7

RUN gem install haml2slim --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["haml2slim"]
CMD ["--help"]
