FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.5

RUN gem install check_graphite --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["check_graphite"]
CMD ["--help"]
