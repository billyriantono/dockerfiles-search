FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.0.4

RUN gem install conf_conf --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["conf_conf"]
CMD ["--help"]
