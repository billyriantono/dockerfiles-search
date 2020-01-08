FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.0

RUN gem install jack-eb --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jack"]
CMD ["--help"]
