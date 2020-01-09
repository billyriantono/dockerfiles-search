FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.9.0

RUN gem install inspec --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["inspec"]
CMD ["--help"]
