FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2.5

RUN gem install CoC-Calc --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["CoC-Calc"]
CMD ["--help"]
