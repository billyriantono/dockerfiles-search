FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=3.0.2

RUN gem install kensa --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["kensa"]
CMD ["--help"]
