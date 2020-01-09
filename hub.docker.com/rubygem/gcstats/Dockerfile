FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.4

RUN gem install gcstats --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gcstats"]
CMD ["--help"]
