FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.0.pre2

RUN gem install js2 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["js2-ruby"]
CMD ["--help"]
