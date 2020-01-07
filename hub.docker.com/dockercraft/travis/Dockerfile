FROM dockercraft/alpine:3.7
MAINTAINER Daniel <daniel@topdevbox.com>

# How-To
 # Local Build: docker build -t travis .
 # Local Run: docker run -it travis travis help

ENV PACKAGES "g++ make ruby ruby-dev ruby-json git"

RUN apk update \
	&& apk upgrade \
	&& apk add --update $PACKAGES \
	&& echo 'gem: --no-document' > /etc/gemrc \
	&& gem install travis \
    && rm -rf /var/cache/apk/*
    
