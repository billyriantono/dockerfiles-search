FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.7.1

RUN gem install auto_excerpt --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["auto_excerpt"]
CMD ["--help"]
