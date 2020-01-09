FROM node:carbon-alpine AS builder

WORKDIR /opt/kontoso/platform/api

# Optimise build times by only copying package.json and package-lock.json before
# running `npm install`
COPY package.json package-lock.json ./
RUN npm install

COPY . .
RUN npm run build

FROM builder

# Remove development dependencies and sources
RUN npm prune --only=production && rm -rf src

ENTRYPOINT ["/usr/local/bin/npm", "start"]
