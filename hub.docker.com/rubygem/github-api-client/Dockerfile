FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.0.pre

RUN gem install github-api-client --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["api-browser.rb"]
CMD ["--help"]
