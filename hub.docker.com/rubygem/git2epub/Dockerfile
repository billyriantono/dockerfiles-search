FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.1

RUN gem install git2epub --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git2epub"]
CMD ["--help"]
