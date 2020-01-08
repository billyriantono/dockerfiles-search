FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.0.0

RUN gem install auto_pilot --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["autopilot"]
CMD ["--help"]
