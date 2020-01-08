FROM ruby:2.3.3-alpine
MAINTAINER J.R. Arseneau <comments@theinterstitial.net>
RUN apk add --update \
	build-base \
	ruby-dev \
	gcc \
	libxml2 \
	libxslt
RUN gem install compass

WORKDIR /src

ENTRYPOINT ["compass"]
