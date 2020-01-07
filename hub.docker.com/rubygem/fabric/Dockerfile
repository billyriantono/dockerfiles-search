FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.4

RUN gem install fabric --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["fab"]
CMD ["--help"]
