FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6.6

RUN gem install contao --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["contao"]
CMD ["--help"]
