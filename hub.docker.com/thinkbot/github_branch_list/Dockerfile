FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6.3

RUN gem install github_branch_list --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["github_branch_list"]
CMD ["--help"]
