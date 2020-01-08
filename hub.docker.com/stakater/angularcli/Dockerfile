FROM stakater/node:6.9
LABEL authors="Rasheed <rasheed@aurorasolutions.io>"

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh && \
    npm install -g @angular/cli