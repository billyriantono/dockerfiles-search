FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=3.3.5

RUN gem install geonames_local --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["geonames"]
CMD ["--help"]
