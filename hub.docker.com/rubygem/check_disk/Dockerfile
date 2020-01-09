FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.4

RUN gem install check_disk --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["check_disk.rb"]
CMD ["--help"]
