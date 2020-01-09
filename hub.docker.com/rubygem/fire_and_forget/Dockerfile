FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.3

RUN gem install fire_and_forget --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["fire_forget"]
CMD ["--help"]
