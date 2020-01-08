FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.3

RUN gem install idclight --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ensembl_to_entrez.rb"]
CMD ["--help"]
