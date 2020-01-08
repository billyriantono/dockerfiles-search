FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.2

RUN gem install git_story --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-story"]
CMD ["--help"]
