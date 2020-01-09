FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.3

RUN gem install bike --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["bike"]
CMD ["--help"]
