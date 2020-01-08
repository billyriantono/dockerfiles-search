FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.8.5

RUN gem install jruby-win32ole --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["make_data.rb"]
CMD ["--help"]
