FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.1

RUN gem install btetris_kp --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["btetris_kp"]
CMD ["--help"]
