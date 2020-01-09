FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.9

RUN gem install kramdown-rfc2629 --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["kramdown-rfc2629"]
CMD ["--help"]
