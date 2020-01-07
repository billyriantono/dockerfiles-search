FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.6

RUN gem install EC2ssh --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ec2ssh"]
CMD ["--help"]
