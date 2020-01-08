FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.1

RUN gem install jruby-lint --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jrlint"]
CMD ["--help"]
