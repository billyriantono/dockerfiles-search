FROM node:6.12.0-alpine

RUN apk --update --no-cache add \
	python \
	make \
	git \
	build-base \
	libstdc++ \
	&& npm install --global @angular/cli \
	&& npm install --global node-sass \
	&& rm -rf /var/cache/apk/*

EXPOSE 4200

WORKDIR /var/www/app

VOLUME ["/var/www/app"]

ENTRYPOINT ["npm"]

CMD ["start"]