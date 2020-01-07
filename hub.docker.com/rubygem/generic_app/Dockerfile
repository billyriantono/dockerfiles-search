FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.0.2

RUN gem install generic_app --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["generic_app"]
CMD ["--help"]
