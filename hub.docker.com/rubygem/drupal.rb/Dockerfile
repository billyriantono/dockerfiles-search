FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.13

RUN gem install drupal.rb --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["drupal"]
CMD ["--help"]
