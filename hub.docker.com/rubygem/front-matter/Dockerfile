FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2.1

RUN gem install front-matter --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["front_matter"]
CMD ["--help"]
