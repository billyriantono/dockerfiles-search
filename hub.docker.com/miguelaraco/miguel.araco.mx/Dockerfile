FROM nginx:alpine

RUN apk add --update \
	bash && \
	rm -rf /var/cache/apk/*

COPY server/default.conf /etc/nginx/conf.d/default.conf

COPY public /usr/share/nginx/html