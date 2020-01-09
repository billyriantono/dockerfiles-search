FROM mhart/alpine-node

RUN apk update
RUN apk add bash
RUN apk add curl
RUN apk add perl
RUN apk add git

RUN npm install sfdx-cli --global

RUN sfdx --version
RUN sfdx plugins --core

RUN apk add perl-config-properties
RUN apk add perl-http-message
RUN apk add perl-json
RUN apk add perl-lwp-useragent-determined
RUN apk add perl-lwp-protocol-https

