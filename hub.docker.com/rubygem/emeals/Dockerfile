FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.4

RUN gem install emeals --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["menu_to_json"]
CMD ["--help"]
