FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2.1

RUN gem install atoulme-Saikuro --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["saikuro"]
CMD ["--help"]
