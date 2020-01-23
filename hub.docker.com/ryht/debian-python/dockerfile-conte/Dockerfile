FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.9.0

RUN gem install kramdown --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["kramdown"]
CMD ["--help"]
