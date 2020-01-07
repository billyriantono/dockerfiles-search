FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.3

RUN gem install jshint4r --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jshint4r"]
CMD ["--help"]
