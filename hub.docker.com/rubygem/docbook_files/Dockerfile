FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.0

RUN gem install docbook_files --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["docbook_files"]
CMD ["--help"]
