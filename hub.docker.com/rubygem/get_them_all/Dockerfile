FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.4

RUN gem install get_them_all --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gta"]
CMD ["--help"]
