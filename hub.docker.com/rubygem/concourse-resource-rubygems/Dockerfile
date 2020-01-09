FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.4

RUN gem install concourse-resource-rubygems --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["check"]
CMD ["--help"]
