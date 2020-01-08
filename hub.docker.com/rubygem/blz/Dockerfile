FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.4.20170306

RUN gem install blz --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["blz"]
CMD ["--help"]
