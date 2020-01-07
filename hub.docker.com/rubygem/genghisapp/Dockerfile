FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.3.9

RUN gem install genghisapp --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["genghisapp"]
CMD ["--help"]
