FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.8.2

RUN gem install djsun-mongo_mapper --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["mmconsole"]
CMD ["--help"]
