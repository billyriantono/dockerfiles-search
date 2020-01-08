FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.0

RUN gem install bamboolab_contact_form --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["bamboolab_contact_form"]
CMD ["--help"]
