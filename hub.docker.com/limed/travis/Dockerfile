FROM ruby:alpine

RUN apk add --no-cache --virtual .build-deps \
	gcc \
	libxslt-dev \
	ruby-dev \
	build-base \
	libffi-dev

RUN gem install travis --no-document && \
	apk add --no-cache git

RUN apk --purge del .build-deps

ENTRYPOINT [ "/usr/local/bundle/bin/travis" ]
