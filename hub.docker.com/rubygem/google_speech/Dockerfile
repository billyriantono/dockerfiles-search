FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.1

RUN gem install google_speech --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["google_speech"]
CMD ["--help"]
