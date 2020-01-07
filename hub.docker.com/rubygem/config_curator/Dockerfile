FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.0

RUN gem install config_curator --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["curate"]
CMD ["--help"]
