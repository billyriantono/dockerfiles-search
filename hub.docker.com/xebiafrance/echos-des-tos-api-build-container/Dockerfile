FROM node:11.14.0-alpine
LABEL maintainer=Horgix
LABEL project=echos-des-tos-api

RUN apk --no-cache add ca-certificates \
      && rm -rf /var/cache/apk/*

RUN mkdir -p /usr/local/bin/node-serverless

COPY package.json       /usr/local/bin/node-serverless/package.json
COPY package-lock.json  /usr/local/bin/node-serverless/package-lock.json

RUN npm install --prefix /usr/local/bin/node-serverless

RUN apk add --update py-pip python3 \
      && rm -rf /var/cache/apk/*

# We need to do that so serverless can find its
# python-serverless-requirements plugin while not impacting working directory
RUN ln -s /usr/local/bin/node-serverless/node_modules /node_modules

ENV PATH="/usr/local/bin/node-serverless/node_modules/.bin:${PATH}"

CMD ["serverless"]
