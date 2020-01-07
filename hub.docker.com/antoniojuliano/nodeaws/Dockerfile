FROM node:8.6.0-alpine

RUN apk update && apk upgrade && \
  	apk -Uuv add make g++ python py-pip git && \
  	pip install awscli && \
  	apk --purge -v del py-pip && \
  	rm /var/cache/apk/*

CMD ["/bin/sh"]
