FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.5

RUN gem install hashtoxml --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hash_to_xml"]
CMD ["--help"]
