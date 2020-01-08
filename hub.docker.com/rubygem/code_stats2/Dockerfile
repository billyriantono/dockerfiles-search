FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.8

RUN gem install code_stats2 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["code_stats"]
CMD ["--help"]
