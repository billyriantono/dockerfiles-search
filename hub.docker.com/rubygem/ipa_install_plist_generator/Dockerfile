FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.0

RUN gem install ipa_install_plist_generator --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ipa_plist_gen"]
CMD ["--help"]
