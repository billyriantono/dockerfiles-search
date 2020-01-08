FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9

RUN gem install di-ruby-lvm-attrib --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["generate_field_data"]
CMD ["--help"]
