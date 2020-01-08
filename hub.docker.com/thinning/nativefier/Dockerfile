FROM alpine:latest

RUN apk update && apk add --no-cache \
	nodejs \
	npm \
	&& npm -g i nativefier \
	&& npm cache clean --force

CMD nativefier