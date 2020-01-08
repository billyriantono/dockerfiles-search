FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.4.1

RUN gem install git-semver-cop --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-semver-cop"]
CMD ["--help"]
