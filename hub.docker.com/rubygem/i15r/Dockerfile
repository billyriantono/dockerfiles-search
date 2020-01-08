FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.5

RUN gem install i15r --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["i15r"]
CMD ["--help"]
