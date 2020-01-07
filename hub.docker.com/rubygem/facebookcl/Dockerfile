FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.1

RUN gem install facebookcl --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["facebook"]
CMD ["--help"]
