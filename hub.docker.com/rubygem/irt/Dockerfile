FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.3.3

RUN gem install irt --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["irt"]
CMD ["--help"]
