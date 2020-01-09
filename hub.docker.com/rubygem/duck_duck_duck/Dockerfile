FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=4.3.0

RUN gem install duck_duck_duck --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["duck_duck_duck"]
CMD ["--help"]
