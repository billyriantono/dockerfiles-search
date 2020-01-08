FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.4.0

RUN gem install google-ime-skk --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["google-ime-skk"]
CMD ["--help"]
