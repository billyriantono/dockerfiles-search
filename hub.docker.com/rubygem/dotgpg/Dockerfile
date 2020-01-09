FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.7.0

RUN gem install dotgpg --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["dotgpg"]
CMD ["--help"]
