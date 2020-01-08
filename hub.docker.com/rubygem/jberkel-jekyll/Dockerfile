FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.7

RUN gem install jberkel-jekyll --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jekyll"]
CMD ["--help"]
