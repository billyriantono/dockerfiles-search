FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.1

RUN gem install image_optim --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["image_optim"]
CMD ["--help"]
