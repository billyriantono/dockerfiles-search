FROM node:6.11.2-alpine
LABEL "maintainer": "adam.berkowitz@uconn.edu" \
      "name": "Adam Berkowitz" \
      "project": "node test"

WORKDIR /project

RUN apk update && apk add bash \
    && npm set progress=false \
    && npm install -g yarn gulp-cli webpack \
    && yarn add --dev --no-progress gulp \ 
    && yarn install \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 3000

ENTRYPOINT ["/bin/bash", "-c"]

