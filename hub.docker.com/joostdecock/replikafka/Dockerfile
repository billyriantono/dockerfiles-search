## Stage 1: Builder
FROM node:alpine as builder

## Set workdir
WORKDIR /replikafka

## Install build toolchain
RUN apk add --no-cache python make g++

## Install node dependencies and compile native add-ons
COPY package* ./
RUN npm install

## Build app
COPY src src
RUN npm run build


## Stage 2: App
FROM node:alpine as app

## Set workdir
WORKDIR /replikafka

## Copy built node modules and binaries without including the toolchain
COPY --from=builder /replikafka/node_modules /replikafka/node_modules/
COPY --from=builder /replikafka/build /replikafka/build

## Create config directory
RUN mkdir -p /etc/replikafka

## Copy config (typically overwritten by mounted volume)
COPY example.config.yml /etc/replikafka/config.yml

## Add a user to run the app
RUN addgroup -S replikafka \
  && adduser -S replikafka \
  && chown -R replikafka /replikafka

## Drop privleges and run app
USER replikafka
CMD ["node",  "./build/main.js"]
