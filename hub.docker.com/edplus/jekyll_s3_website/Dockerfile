FROM ruby:2.4.1-alpine

LABEL maintainer=chandi<chandima@asu.edu>

ENV JEKYLL_VERSION      	3.5.2
ENV HTML_PROOFER_VERSION	3.7.2
ENV S3_WEBSITE_VERSION  	3.2.0

RUN apk add --update bash build-base openjdk7-jre

RUN gem install s3_website -v $S3_WEBSITE_VERSION
RUN gem install jekyll -v $JEKYLL_VERSION
RUN gem install html-proofer -v $HTML_PROOFER_VERSION