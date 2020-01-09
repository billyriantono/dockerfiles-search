FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.5

RUN gem install joyent --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["joyent"]
CMD ["--help"]
