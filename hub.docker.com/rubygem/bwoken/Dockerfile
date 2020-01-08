FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.1.0.rc.2

RUN gem install bwoken --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["unix_instruments.sh"]
CMD ["--help"]
