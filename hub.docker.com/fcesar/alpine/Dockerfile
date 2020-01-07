FROM fcesar/alpine

###
RUN apk add --update --progress --no-cache ruby \
	&& rm  -rf /tmp/* \
	&& rm -rf /var/cache/apk/* \
	&& ruby --version