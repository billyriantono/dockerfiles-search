FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.2

RUN gem install appmake --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["appmake"]
CMD ["--help"]
