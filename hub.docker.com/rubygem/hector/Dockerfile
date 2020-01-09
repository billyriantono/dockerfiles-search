FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.9

RUN gem install hector --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hector"]
CMD ["--help"]
