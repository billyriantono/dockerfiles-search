FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.3

RUN gem install jbundler --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jbundle"]
CMD ["--help"]
