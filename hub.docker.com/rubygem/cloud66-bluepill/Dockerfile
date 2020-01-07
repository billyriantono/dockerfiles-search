FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.64

RUN gem install cloud66-bluepill --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["bluepill"]
CMD ["--help"]
