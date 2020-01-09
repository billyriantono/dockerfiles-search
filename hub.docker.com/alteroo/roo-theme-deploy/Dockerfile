FROM node:lts-alpine
MAINTAINER David Bain "david.bain@alteroo.com"

RUN npm install -g less; npm install -g plonetheme-upload
RUN apk update && apk upgrade && apk add bash && rm -rf /var/cache/*/*
RUN sed -i -e "s/bin\/ash/bin\/bash/" /etc/passwd

ENV LC_ALL=en_US.UTF-8
