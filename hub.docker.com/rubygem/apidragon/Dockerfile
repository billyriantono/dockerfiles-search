FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.8.0

RUN gem install apidragon --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["apidragon"]
CMD ["--help"]
