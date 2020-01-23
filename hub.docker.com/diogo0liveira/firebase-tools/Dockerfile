FROM node:13.6.0-alpine3.11
LABEL maintainer="Diogo Oliveira <diogo0liveira@hotmail.com>"

ENV LANG='en_US.UTF-8' \
    LANGUAGE='en_US:en' \
    LC_ALL='en_US.UTF-8'

RUN apk add --update --no-cache \
    bash && \
	rm -rf /tmp/* && \
	rm -rf /var/cache/apk/*

RUN npm install -g firebase-tools   

CMD ["/bin/sh"]