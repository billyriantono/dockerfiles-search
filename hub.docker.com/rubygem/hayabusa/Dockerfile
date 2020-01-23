FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9

RUN gem install hayabusa --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["check_running.rb"]
CMD ["--help"]
