FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.4.3

RUN gem install cloudformation-ruby-dsl --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cfntemplate-to-ruby"]
CMD ["--help"]
