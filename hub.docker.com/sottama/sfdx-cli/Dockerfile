
FROM node:alpine

LABEL   Author=julio.lima@sottama.com \
        Name=docker-sfdx-cli \
        Version=0.0.1

RUN apk --update --no-cache add bash openssl ca-certificates

RUN npm install sfdx-cli --global && \
    sfdx update
	
RUN sfdx --version && \
    sfdx plugins --core