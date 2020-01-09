FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.5.1

RUN gem install jist --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jist"]
CMD ["--help"]
