FROM ruby:2.4.1-alpine3.6

LABEL maintainer=chandi<chandima@asu.edu>

ENV JEKYLL_VERSION      3.7.3
ENV S3_WEBSITE_VERSION  3.4.0

RUN apk add --update bash build-base nodejs nodejs-npm chromium chromium-chromedriver openjdk7-jre git

RUN gem install s3_website -v $S3_WEBSITE_VERSION
RUN s3_website install
RUN gem install jekyll -v $JEKYLL_VERSION