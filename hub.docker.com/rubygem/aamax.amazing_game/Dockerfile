FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.1

RUN gem install aamax.amazing_game --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["studio_game"]
CMD ["--help"]
