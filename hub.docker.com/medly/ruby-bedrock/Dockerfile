# ---- Base ----
FROM ruby:2.6.5-alpine AS base

# core dependencies needed
RUN apk --no-cache add build-base postgresql-dev nodejs yarn tzdata
#Building nokogiri and pg take a while, do it now before installing the rest of the gems
RUN gem install nokogiri -v 1.10.4
RUN gem install pg -v 1.1.4
