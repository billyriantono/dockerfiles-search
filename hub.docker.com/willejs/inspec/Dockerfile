FROM ruby:2.1

ARG INSPEC_VERSION=1.14.1

RUN gem install inspec -v ${INSPEC_VERSION} --no-ri --no-rdoc

RUN mkdir /home/inspec

WORKDIR /home/inspec

CMD inspec exec ./
