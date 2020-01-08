FROM ruby:2.6.3-alpine
MAINTAINER Amoux Kin <amouxkin@gmail.com>

# Base packages
RUN apk add --no-cache \
      build-base \
      libxml2-dev \
      libxslt-dev \
      postgresql-dev \
      nodejs \
      tzdata \
      bash \
      yarn
      
RUN gem install rails && gem install postgres

# ENV project=move-and-groove
# RUN cd home && mkdir workspace
# WORKDIR /home/workspace/$project

EXPOSE 3000

ENTRYPOINT bash
