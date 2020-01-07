FROM alpine:latest

ENV TMPDIR $(mktemp -d -t ci-XXXXXXXXXX)
ENV ISUSER `$(id -u www-data > /dev/null 2>&1; echo $?)`
ENV ISGRP `$(id -g www-data > /dev/null 2>&1; echo $?)`

VOLUME onion-shared_code:/code

RUN 	set -e; \
	export  TMPDIR=$(mktemp -d -t ci-XXXXXXXXXX) ; \
	if [ ! $ISGRP eq 0 ]; then "addgroup -g 82 www-data"; fi \
	&& if [ ! $ISUSER eq 0 ]; then "adduser -D -u 82 -G www-data www-data"; fi \
	&& apk add --no-cache --virtual build-tools gnupg git \
	&& if [ ! -d $TMPDIR ]; then exit 1; fi \
	&& cd $TMPDIR \
	&& git init . \
	&& git config --global user.name nixroxursox \
	&& git config --local user.email siteadmin@site.onion \
	&& git clone https://nixroxursox:ts-5010l@github.com/nixroxursox/website.git \
	&& chown -R 82:82 website \ 
	&& mv website /code; \
	apk del build-tools && rm -rf $TMPDIR

	
ENTRYPOINT ["tail", "-f", "/dev/null" ]
