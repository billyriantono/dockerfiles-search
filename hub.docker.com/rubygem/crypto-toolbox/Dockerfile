FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.5

RUN gem install crypto-toolbox --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["break-vigenere-xor"]
CMD ["--help"]
