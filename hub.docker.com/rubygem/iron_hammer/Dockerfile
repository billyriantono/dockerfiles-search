FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.1

RUN gem install iron_hammer --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ivy"]
CMD ["--help"]
