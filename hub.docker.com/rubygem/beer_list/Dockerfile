FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.0.0.rc1

RUN gem install beer_list --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["beer_list"]
CMD ["--help"]
