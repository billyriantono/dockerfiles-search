FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.1

RUN gem install git_spelunk --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-spelunk"]
CMD ["--help"]
