FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.1

RUN gem install git_er_done --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gd"]
CMD ["--help"]
