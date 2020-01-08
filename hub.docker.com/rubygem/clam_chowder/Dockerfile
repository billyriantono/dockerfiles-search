FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.1

RUN gem install clam_chowder --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["clam_chowder"]
CMD ["--help"]
