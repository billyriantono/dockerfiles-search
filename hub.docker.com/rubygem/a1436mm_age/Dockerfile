FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.1

RUN gem install a1436mm_age --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["a1436mm_age"]
CMD ["--help"]
