FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.6

RUN gem install gcov2x --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gcov2x"]
CMD ["--help"]
