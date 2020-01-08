FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.2

RUN gem install 3months_staff_schedule --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["staff_schedule"]
CMD ["--help"]
