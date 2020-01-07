FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.3

RUN gem install js_spec --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["js_spec"]
CMD ["--help"]
