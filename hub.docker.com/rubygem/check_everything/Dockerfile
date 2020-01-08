FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.3

RUN gem install check_everything --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["check_everything"]
CMD ["--help"]
