FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.4

RUN gem install factory_girl_upgrader --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["factory_girl_upgrader"]
CMD ["--help"]
