FROM ruby:alpine
LABEL maintainer "iilness <andre.aliaman90@gmail.com>"

ENV LANG "en_US.UTF-8"
ENV LANGUAGE "en_US.UTF-8"
ENV LC_ALL "en_US.UTF-8"

RUN deluser guest ; delgroup users

RUN mkdir workdir
WORKDIR workdir
RUN apk add --update g++ make
RUN gem install fastlane


USER root
