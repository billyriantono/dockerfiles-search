FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=3.2.1

RUN gem install gemnasium --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gemnasium"]
CMD ["--help"]
