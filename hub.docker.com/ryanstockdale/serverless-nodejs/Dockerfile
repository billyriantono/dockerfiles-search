FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.4

RUN gem install jekyll_pages_api_search --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jekyll_pages_api_search"]
CMD ["--help"]
