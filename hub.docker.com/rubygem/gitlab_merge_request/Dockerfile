FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.0

RUN gem install gitlab_merge_request --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-mr"]
CMD ["--help"]
