FROM ruby:2.6-stretch as builder
LABEL author="Andrew Porter <partydrone@icloud.com>"

ENV RAILS_MAJOR 5.2
ENV RAILS_VERSION 5.2.3

RUN gem install rails -v ${RAILS_VERSION}

ENTRYPOINT [ "rails" ]
CMD [ "-h" ]
