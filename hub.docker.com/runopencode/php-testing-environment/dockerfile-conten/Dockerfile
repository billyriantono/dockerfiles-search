FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.9.0

RUN gem install github_changelog_generator --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ghclgen"]
CMD ["--help"]
